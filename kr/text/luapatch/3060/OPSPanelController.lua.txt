local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)

local ShowItemLimitUINew = function(self,itemids)
	self:ShowItemLimitUINew(itemids);
	if self.itemuiObjNew ~= nil and not self.itemuiObjNew:isNull() then
		local itemabout = self.item_use:GetDataById(itemids[0]);
		local num0 = itemabout.iteminfo.active_dailyLimit_num;
		local num1 = itemabout.ItemTodayCanGet;
		local bar = self.itemuiObjNew.transform:Find("Bar");
		if bar ~= nil then
			local image = bar:GetComponent(typeof(CS.ExImage));
			if num0 ~= 0 then
				image.fillAmount = num1*1.0/num0;
			else
				image.fillAmount = 0;
			end
		end
		local showTipObj =self.itemuiObjNew.transform:Find("TouchArea");
		if showTipObj ~= nil then
			local tip = showTipObj:GetComponent(typeof(CS.CommonShowTip));
			local language = CS.Data.GetLang(60826);
			local tipText = CS.System.String.Format(language, tostring(num1));
			tip.strIntroduction = tipText;
			tip.strTitle = itemabout.iteminfo.name;
		end
	end
end

local InitPanelSpot = function(self,spot)
	self.panelSpot = spot;
	self.mission = spot.mission;
	self.opsMission = spot.opsMission;
	self.missionInfo = spot.missionInfo;
	self.entranceId = spot.opsMission.entranceId;
	self:RefreshEntranceUI();
	self:RefresCommonUI();
	if self.opsMission ~= nil then
		self:ShowNewReward();
	else
		self:ShowOldReward();
	end
	self:CheckInfoPos();
end

local LoadLeftBG = function(self)
	if not CS.OPSConfig.Instance.OPSLeftBGNormalActivity:ContainsKey(self.campaionId) then
		return;
	end
	local path = "Pics/ActivityMap/"..CS.OPSConfig.Instance.OPSLeftBGNormalActivity[self.campaionId];
	local bgObj = CS.ResManager.GetObjectByPath(path);
	if bgObj == nil then
		return;
	end
	local bg = CS.UnityEngine.GameObject.Instantiate(bgObj);
	bg.transform:SetParent(self.leftMain, false);
	bg.transform:SetAsFirstSibling();
end

local PlayMove = function(self)
	if self.groupInfo ~= nil then
		self.opsMission = CS.OPSMission();
		self.opsMission.missionIds:Add(self.CurrentMissionId);
	end
	self:PlayMove();
end

local SelectMissionSpot = function(self,spot)
	if self.chooseSpot ~= nil then
		self:CancelMission();
		CS.CommonController.Invoke(function()
				self:SelectMissionSpot(spot);
			end,0.3,self);
	else
		self:SelectMissionSpot(spot);
	end
end
local chooseing = function(self)
	return self.currentChoose ~= nil;
end
local RequestBOBreakoutStartMissionHandle = function(self,result)
	local mission = CS.GameData.listMission:GetDataById(result.missionid);
	mission.counter = mission.counter + 1;
	self:RequestBOBreakoutStartMissionHandle(result);
end
local TriggerEndDragHandler = function(self,eventData)
	self:TriggerEndDragHandler(eventData);
	if CS.OPSPanelController.Instance.chooseSpot ~= nil then
		CS.OPSPanelController.Instance:CancelMission();
	end
end
local CanChooseDrag = function(self)
	if self.chooseSpot ~= nil then
		return false;
	end
	return self:CanChooseDrag();
end
local ShowReward = function(self,missionid)
	self:ShowReward(missionid);
	local mission = CS.GameData.listMission:GetDataById(missionid);
	local getIcon = self.breakoutMissionObj.transform:Find("Main/MissionPart/MainRewardIcon/GetIcon");
	if getIcon ~= nil then
		getIcon.transform:SetAsLastSibling();
		getIcon.gameObject:SetActive(mission.winCount>0);
	end
end
local RequestBOBreakoutOrganizePackageHandle = function(self,request)
	self:RequestBOBreakoutOrganizePackageHandle(request);
	if CS.GF.Tarkov.GameDataCache.I.playerData.nextPhaseInfo == nil then
		local missionid = CS.GF.Tarkov.GameDataCache.I.playerData.missionId;
		local mission = CS.GameData.listMission:GetDataById(missionid);
		mission.winCount = mission.winCount + 1;
	end
end
util.hotfix_ex(CS.OPSPanelController,'ShowItemLimitUINew',ShowItemLimitUINew)
util.hotfix_ex(CS.OPSPanelController,'LoadLeftBG',LoadLeftBG)
util.hotfix_ex(CS.OPSPanelController,'SelectMissionSpot',SelectMissionSpot)
util.hotfix_ex(CS.OPSPanelController,'get_chooseing',chooseing)
util.hotfix_ex(CS.OPSPanelController,'RequestBOBreakoutStartMissionHandle',RequestBOBreakoutStartMissionHandle)
util.hotfix_ex(CS.SpecialMissionInfoController,'InitPanelSpot',InitPanelSpot)
util.hotfix_ex(CS.OPSPanelMissionHolder,'PlayMove',PlayMove)
--util.hotfix_ex(CS.OPSPanelBackGround,'TriggerEndDragHandler',TriggerEndDragHandler)
util.hotfix_ex(CS.OPSPanelController,'CanChooseDrag',CanChooseDrag)
util.hotfix_ex(CS.OPSPanelController,'ShowReward',ShowReward)
util.hotfix_ex(CS.BreakoutPhaseBattleFinishController,'RequestBOBreakoutOrganizePackageHandle',RequestBOBreakoutOrganizePackageHandle)


local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)
xlua.private_accessible(CS.OPSPanelSpot)
xlua.private_accessible(CS.OPSLetterReceiveController)

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
	return false;
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
local LoadLetterUI = function(self)
	if self.currentPanelConfig.letterConfig ~= nil then
		if not self.currentPanelConfig.letterConfig.isSendLetter then
			local missionid = self.currentPanelConfig.letterConfig.missionid;
			local mission = CS.GameData.listMission:GetDataById(missionid);
			if mission == nil or mission.UseWinCounter ==0 then
				return;
			end
		end
	end
	self:LoadLetterUI();
	if self.currentPanelConfig.letterConfig ~= nil then
		if not self.currentPanelConfig.letterConfig.isSendLetter then
			local check = CS.UnityEngine.PlayerPrefs.GetInt("isLetterShow", 0);
			if check == 0 then
				self:ShowLetterEvent();
				CS.UnityEngine.PlayerPrefs.SetInt("isLetterShow", 1);
				CS.UnityEngine.PlayerPrefs.Save();
			end
		end	
	end
end
local RequestSetDrawEvent = function(self,data)
	self:CheckAllTimelineState();
	self:RequestSetDrawEvent(data);
end
local CheckAllTimelineState = function(self)
	if self.campaionId ~= -74 then
		self:CheckAllTimelineState();
		return;
	end
	if self.currentPanelConfig.oPSUnclockTimeLines.Keys.Count == 0 then
		return;
	end
	local iter = self.currentPanelConfig.oPSUnclockTimeLines:GetEnumerator(); 	
	while iter:MoveNext() do 
		local scenePath = iter.Current.Key;
		local timelines = iter.Current.Value;
		local timeTrans = self.transform.parent:Find(scenePath);
		local playableDirector = timeTrans:GetComponent(typeof(CS.UnityEngine.Playables.PlayableDirector));
		playableDirector.playOnAwake = false;
		local hascheck = false;
		print(scenePath);
		for j=timelines.Count-1,0,-1 do
			if not hascheck then
				local timeline = timelines[j];
				local checkState = false;
				local ids = CS.System.Collections.Generic.List(CS.System.Int32)(timeline.order);
				if timeline.type == -1 then
					for m = 0,ids.Count-1 do
						local mission = CS.GameData.listMission:GetDataById(ids[m]);
						if mission ~= nil then
							print(ids[m]);
							checkState = true;
						end
					end
				end
				if checkState then
					local check = self:CheckTimeLineState(playableDirector, timeline.timelinePath);
					if check then
						hascheck = true;
					end
				end
			end
		end
		if not hascheck then
			if timelines.Count > 0 then
				self:CheckTimeLineStart(playableDirector, timelines[0].timelinePath);    
			end
		end
	end
end
local ShowLetterList = function(self)
	if not self.currentPanelConfig.letterConfig.isSendLetter then
		CS.UnityEngine.PlayerPrefs.SetInt("isFirstLetterTip", 1);
		CS.UnityEngine.PlayerPrefs.Save();
	end
	self:ShowLetterList();
end
local PlaySpotLine = function(self,play,delay,playUnclock)
	local time = 0;
	for i=0,self.lastSpots.Count-1 do
		local lastSpot = self.lastSpots[i];
		if lastSpot.CanShow then
			for j=0,self.paths.Count-1 do
				local path = self.paths[j];
				if path.oPSPanelSpot0 == lastSpot then
					local show = true;
					if path.showType == 1 then
						if not self.mission.showNewTag then
							path:Hide(play,delay);
							show = false;
						end
					end
					if show then
						if playUnclock then
							time = path:PlayUnClockShow(play,self.playUnclockLineTime, delay);
						else
							path:Show(play,delay);	
						end
					end				
				end
			end
		end
	end
	return time;
end
local CloseUI = function(self)
	if self.timelineReceive ~= nil and not self.timelineReceive:isNull() then
		return;
	end
	self:CloseUI();
end
local RefreshCurrentDiffcluty = function(self)
	local pos = nil;
	local findspot = nil;
	if self.chooseSpot ~= nil and self.chooseSpot.opsMission.missionIds.Count ==1 then
		findspot = self.chooseSpot;
		self.MissionInfoController.gameObject:SetActive(false);
		pos = self.chooseSpot.transform.localPosition;
		for i=0,CS.OPSPanelBackGround.Instance.all3dSpots.Count-1 do
			local spot = CS.OPSPanelBackGround.Instance.all3dSpots:GetDataByIndex(i);
			if spot.transform.localPosition == pos and spot.difficulty == CS.OPSPanelController.difficulty then
				findspot = spot;
			end
		end
	end	
	self:RefreshCurrentDiffcluty();
	if findspot ~= nil then
		self:TriggerSelectOPSSpot(findspot);
		--self:SelectMissionSpot(findspot);
		self.MissionInfoController.gameObject:SetActive(true);
		self.MissionInfoController:InitOPSMission(findspot.opsMission);
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
util.hotfix_ex(CS.OPSPanelController,'LoadLetterUI',LoadLetterUI)
util.hotfix_ex(CS.OPSPanelController,'RequestSetDrawEvent',RequestSetDrawEvent)
util.hotfix_ex(CS.OPSPanelController,'CheckAllTimelineState',CheckAllTimelineState)
util.hotfix_ex(CS.OPSPanelController,'ShowLetterList',ShowLetterList)
util.hotfix_ex(CS.OPSPanelController,'RefreshCurrentDiffcluty',RefreshCurrentDiffcluty)
util.hotfix_ex(CS.BreakoutPhaseBattleFinishController,'RequestBOBreakoutOrganizePackageHandle',RequestBOBreakoutOrganizePackageHandle)
util.hotfix_ex(CS.OPSPanelSpot,'PlaySpotLine',PlaySpotLine)
util.hotfix_ex(CS.OPSLetterReceiveController,'CloseUI',CloseUI)


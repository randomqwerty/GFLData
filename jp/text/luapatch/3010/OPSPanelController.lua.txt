local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)
xlua.private_accessible(CS.OPSConfig)
xlua.private_accessible(CS.OPSPanelBackGround)
xlua.private_accessible(CS.CommonSceneManagerController)
xlua.private_accessible(CS.CommonController)
xlua.private_accessible(CS.ExButton)
xlua.private_accessible(CS.ResManager)
xlua.private_accessible(CS.OPSPanelConfig)
xlua.private_accessible(CS.OPSSpineMission)
local SelectModuleSpine = function(self,spinecontrol)
	self:CancelSelectMoudleSpine();
	self:SelectModuleSpine(spinecontrol);
end
local checkcode;
local ShowOPSSpineMissionUI = function(self,code)
	self:ShowOPSSpineMissionUI(code);
	if not self.currentPanelConfig.opsSpineMissions:ContainsKey(code) then
		return;
	end
	checkcode = code;
	print(code);
	local spineMission = self.currentPanelConfig.opsSpineMissions:get_Item(code);
	if not self.moudleSpineUIObj.gameObject.activeInHierarchy then
		local childItem = self.moudleSpineUIObj.transform:Find(self.currentPanelConfig.moudleSpineUI.itemPath);
		for i=0,childItem.parent.childCount-1 do
			if i> spineMission.opsMissions.Count then
				childItem.parent:GetChild(i).gameObject:SetActive(false);
			end
		end
		self.useOPSmissions:Clear();
		local trans = self.panalMissionTrans:GetEnumerator();
		while trans:MoveNext() do
			local key = trans.Current.Key;
			local value = trans.Current.Value;
			self:CheckOPSMissionItem(key,value);
			if value.gameObject.activeSelf then
				self.useOPSmissions:Add(key);
			end
		end
		self.num = self.useOPSmissions.Count;
		self.checkPosMax = self.currentPanelConfig.moudleSpineUI.selectPosX;
		self.distance = self.currentPanelConfig.moudleSpineUI.eachDistance;
		self.moudleSpineUIObj.gameObject:SetActive(true);
	end
	self:CheckEndlessPoint();
end
local HideOPSSpineMissionUI = function(self)
	self:HideOPSSpineMissionUI();
	self:CheckEndlessPoint();
end
local CanGetPoint = function(self,itemid)
	if CS.MissionSelectionController.normalActivityCampaion:Contains(self.campaionId) then
		return true;
	end
	return self:CanGetPoint(itemid);
end
local myLoadReturn = function(self)
	if (CS.OPSConfig.Instance.OPSCamapionReturn:ContainsKey(self.campaionId)) then
		return self:LoadReturn();
	else
		local Obj = CS.ResManager.GetObjectByPath(string.format("Pics/ActivityMap/%s", CS.OPSConfig.Instance.OPSReturn));
		if (Obj ~= nil) then
			local returnObject = CS.UnityEngine.Object.Instantiate(Obj):GetComponent(typeof(CS.ExButton));
			returnObject.transform:SetParent(self.Top, false);
			returnObject.transform:SetAsLastSibling();
			returnObject:AddOnClickBack(function ()
					CS.OPSPanelBackGround.Instance:SaveRecord();
					CS.CommonSceneManagerController.instance:PopController();
					CS.CommonController.GotoScene("MissionSelection");
			end);
		end
	end
end

local noticeElse;
local CheckEndlessPoint = function(self)
	if self.campaionId == -54 then
		if self.moudleSpineUIObj ~= nil and self.moudleSpineUIObj.activeInHierarchy and checkcode == "R_RPK16"then
			self:CheckEndlessPoint();
			if self.highScoreObj ~= nil then
				self.highScoreObj:SetActive(true);
			end
			if self.highScoreTotalObj ~= nil then
				self.highScoreTotalObj:SetActive(true);
			end
			if noticeElse == nil then
				noticeElse = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Pics/ActivityMap/2022Summer_HoleNotice"), self.leftMain, false);	
				local txt = noticeElse.transform:Find("URL"):GetComponent(typeof(CS.ExText));
				local url = txt.text;
				local btn = noticeElse:GetComponent(typeof(CS.ExButton));
				btn:AddOnClick(function ()
					self:OpenAnnouncement(url);
				end);	
			end
			if noticeElse ~= nil and not noticeElse:isNull() then
				noticeElse:SetActive(true);
			end
		else
			if self.highScoreObj ~= nil then
				self.highScoreObj:SetActive(false);
			end
			if self.highScoreTotalObj ~= nil then
				self.highScoreTotalObj:SetActive(false);
			end
			if noticeElse ~= nil and not noticeElse:isNull() then
				noticeElse:SetActive(false);
			end
		end
	else
		self:CheckEndlessPoint();
	end
end

local CancelSelectMoudleSpine = function(self)
	self:CancelSelectMoudleSpine();
	self:CancelMission();
end

local CheckMoudleUiTween = function(self)
	local title = self.toggleTitle;
	self.toggleTitle = self.transform;
	self:CheckMoudleUiTween();
	self.toggleTitle = title;
end

local RefreshMoudleBuildUI = function(self)
	local trans = self.panalMissionTrans:GetEnumerator();
	while trans:MoveNext() do
		local key = trans.Current.Key;
		local value = trans.Current.Value;		
		if key.currentMission ~= nil then
			self.missionBaseFinal = value;
		end
	end
	
	self:RefreshMoudleBuildUI();	
end

local CancelMission = function(self)
	self:CancelMission();
	self:RefreshMoudleBuildUI();
end
util.hotfix_ex(CS.OPSPanelController,'SelectModuleSpine',SelectModuleSpine)
util.hotfix_ex(CS.OPSPanelController,'ShowOPSSpineMissionUI',ShowOPSSpineMissionUI)
util.hotfix_ex(CS.OPSPanelController,'HideOPSSpineMissionUI',HideOPSSpineMissionUI)
util.hotfix_ex(CS.OPSPanelController,'CanGetPoint',CanGetPoint)
util.hotfix_ex(CS.OPSPanelController,'LoadReturn',myLoadReturn)
util.hotfix_ex(CS.OPSPanelController,'CheckEndlessPoint',CheckEndlessPoint)
util.hotfix_ex(CS.OPSPanelController,'CancelSelectMoudleSpine',CancelSelectMoudleSpine)
util.hotfix_ex(CS.OPSPanelController,'CheckMoudleUiTween',CheckMoudleUiTween)
util.hotfix_ex(CS.OPSPanelController,'RefreshMoudleBuildUI',RefreshMoudleBuildUI)
util.hotfix_ex(CS.OPSPanelController,'CancelMission',CancelMission)

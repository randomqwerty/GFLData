local util = require 'xlua.util'
local panelController = require("2080/OPSPanelController")
xlua.private_accessible(CS.SpecialMissionInfoController)

local RequestAbortMissionHandle = function(self,www)
	self:RequestAbortMissionHandle(www);
	if CS.OPSPanelController.Instance ~= nil then
		if  CS.OPSPanelController.Instance.clockSelectRing ~= nil and not CS.OPSPanelController.Instance.clockSelectRing:isNull() then
			local control = CS.OPSPanelController.Instance.clockSelectRing.transform:Find("Ring"):GetComponent(typeof(CS.ImageRotateControl));
			missionIdrecord = 0;
			control.checkSelectValue = true;
		end
	end
end

local RefresCommonUI = function(self) 
	if self.entranceId ~= 0 then
		local missionid = self.missionInfo.Id;
		local info = CS.OPSConfig.missionEntranceInfos[self.entranceId];
		self.btnSelectDiffcluty.gameObject:SetActive(false);
		for i=0,info.missionids.Count-1 do
			if info.missionids[i]:Contains(missionid) then
				local check = 0;
				for j=0,info.missionids[i].Count-1 do
					if info.missionids[i][j] == missionid then
						check = check+1;
					end
				end
				if check == 1 then
					self.btnSelectDiffcluty.gameObject:SetActive(true);
				end
			end
		end
	end
	self:RefresCommonUI();
end

local ShowNewReward = function(self)
	local temp1 = CS.Data.GetLang(60048);
	--local temp2 = CS.Data.GetLang(60049);
	--local temp3 = CS.Data.GetLang(60050);
	if self.missionInfo.campaign == -32 then
		local mapMission = CS.GameData.listMissionMapInfo:GetDataById(self.missionInfo.mapped_mission_id);
		if mapMission ~= nil then
			local missionids = mapMission.missionids;
			if missionids.Count == 2 then
				local mission0 = CS.GameData.listMission:GetDataById(missionids[0]);
				local mission1 = CS.GameData.listMission:GetDataById(missionids[1]);
				if mission1 ~= nil and mission0 ~= nil and mission1.winCount == 0 then
					mission1.mappedwincounter = 0;
				end
			end
			if missionids.Count == 3 then
				local mission0 = CS.GameData.listMission:GetDataById(missionids[0]);
				local mission1 = CS.GameData.listMission:GetDataById(missionids[1]);
				local mission2 = CS.GameData.listMission:GetDataById(missionids[2]);
				if mission1 ~= nil and mission0 ~= nil and mission2 ~= nil then
					if mission2.winCount == 0 then
						mission2.mappedwincounter = 0;
					end
					if mission1.winCount == 0 and mission2.winCount == 0 then
						mission1.mappedwincounter = 0;
					end
				end			
			end
			local index = missionids:IndexOf(self.missionInfo.id);
			if index == 0 then
				CS.GameData.listLanguageInfo[60048].content = CS.Data.GetLang(60291);
			elseif index == 1 then
				CS.GameData.listLanguageInfo[60048].content = CS.Data.GetLang(60048);
			elseif index == 2 then
				CS.GameData.listLanguageInfo[60048].content = CS.Data.GetLang(60292);
			end
		else 
			CS.GameData.listLanguageInfo[60048].content = CS.Data.GetLang(60291);
		end
		--CS.GameData.listLanguageInfo[60049].content = CS.Data.GetLang(60048);
		--CS.GameData.listLanguageInfo[60050].content = CS.Data.GetLang(60292);
	end
	self:ShowNewReward();
	if self.missionInfo.campaign == -32 then
		CS.GameData.listLanguageInfo[60048].content = temp1;
		--CS.GameData.listLanguageInfo[60049].content = temp2;
		--CS.GameData.listLanguageInfo[60050].content = temp3;
	end
end

local ShowDrop = function(self)
	while self.expectedGunIconHolder.childCount > 0 do
		CS.UnityEngine.Object.DestroyImmediate(self.expectedGunIconHolder:GetChild(0).gameObject);
	end
	self:ShowDrop();
end

local InitUIElements = function(self)
	self:InitUIElements();
	local txt1 = self.transform:Find("Groove/MultiMission/Tex_Info"):GetComponent(typeof(CS.ExText));
	txt1.text = CS.Data.GetLang(60097);
end
util.hotfix_ex(CS.SpecialMissionInfoController,'RequestAbortMissionHandle',RequestAbortMissionHandle)
util.hotfix_ex(CS.SpecialMissionInfoController,'ShowNewReward',ShowNewReward)
util.hotfix_ex(CS.SpecialMissionInfoController,'ShowDrop',ShowDrop)
util.hotfix_ex(CS.SpecialMissionInfoController,'RefresCommonUI',RefresCommonUI)
util.hotfix_ex(CS.SpecialMissionInfoController,'InitUIElements',InitUIElements)

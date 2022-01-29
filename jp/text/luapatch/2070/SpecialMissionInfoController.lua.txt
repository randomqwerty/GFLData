local util = require 'xlua.util'
local panelController = require("2070/OPSPanelController")
xlua.private_accessible(CS.SpecialMissionInfoController)
local FinishAVG = function(self)
	self:FinishAVG();
	if self.panelMission ~= nil and not self.panelMission:isNull() then
		self.panelMission:ShowNewTag();
	end
	if CS.OPSRuler.Instance ~= nil and not CS.OPSRuler.Instance:isNull() then
		CS.OPSRuler.Instance:InitRulerAvg();
	end
end

local ShowCurrentMission = function(self,missionId)
	self.mission = CS.GameData.listMission:GetDataById(missionId);
	ShowMissionPanel(CS.OPSPanelController.Instance,self.mission);
	CS.CommonAudioController.PlayUI("UI_selete_2");
end

local InitUIElements = function(self)
	self:InitUIElements();
	local txt1 = self.transform:Find("Groove/MultiMission/Tex_Info"):GetComponent(typeof(CS.ExText));
	txt1.text = CS.Data.GetLang(60097);
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
	self.ClearTag.gameObject:SetActive(false);
	self.ClearwhiteTag.gameObject:SetActive(false);
	self:ShowNewReward();
end
local RefreshEntranceUI = function(self)
	self.showtxt:Find("txtTitle").gameObject:SetActive(self.entranceId==0);
	self:RefreshEntranceUI();
end
util.hotfix_ex(CS.SpecialMissionInfoController,'FinishAVG',FinishAVG)
util.hotfix_ex(CS.SpecialMissionInfoController,'ShowCurrentMission',ShowCurrentMission)
util.hotfix_ex(CS.SpecialMissionInfoController,'InitUIElements',InitUIElements)
util.hotfix_ex(CS.SpecialMissionInfoController,'RefresCommonUI',RefresCommonUI)
util.hotfix_ex(CS.SpecialMissionInfoController,'ShowNewReward',ShowNewReward)
util.hotfix_ex(CS.SpecialMissionInfoController,'RefreshEntranceUI',RefreshEntranceUI)
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
local missionInfo = nil;
local RefresCommonUI = function(self)
	if self.missionInfo == missionInfo then
		return;
	end
	missionInfo = self.missionInfo; 
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
util.hotfix_ex(CS.SpecialMissionInfoController,'RequestAbortMissionHandle',RequestAbortMissionHandle)
util.hotfix_ex(CS.SpecialMissionInfoController,'ShowNewReward',ShowNewReward)


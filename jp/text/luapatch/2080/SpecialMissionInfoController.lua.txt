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
util.hotfix_ex(CS.SpecialMissionInfoController,'RequestAbortMissionHandle',RequestAbortMissionHandle)
--util.hotfix_ex(CS.SpecialMissionInfoController,'RefresCommonUI',RefresCommonUI)


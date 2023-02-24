local util = require 'xlua.util'
xlua.private_accessible(CS.SpecialMissionInfoController)

local RefreshEntranceUI = function(self)
	self:RefreshEntranceUI();
	if CS.OPSPanelController.Instance ~= nil then
		if CS.OPSPanelController.Instance.campaionId == -41 then
			self.btnSelectDiffcluty.gameObject:SetActive(false);
		end
	end
end

local RefresCommonUI = function(self)
	self:RefresCommonUI();
	if self.missionInfo.ShowScore then
		self.BossGroove.gameObject:SetActive(false);
	end
end

local GotoDeployment = function(self)
	if CS.OPSPanelController.Instance ~= nil then
		if not CS.OPSPanelController.Instance.CanClick then
			return;
		end
	end
	self:GotoDeployment();
	if CS.OPSPanelController.Instance ~= nil then
		CS.OPSPanelController.Instance.CanClick = false;
	end
end

local RequestStartMissionHandle = function(self,json)
	self:RequestStartMissionHandle(json);
	if CS.OPSPanelController.Instance ~= nil then
		CS.OPSPanelController.Instance.CanClick = true;
	end
end
util.hotfix_ex(CS.SpecialMissionInfoController,'RefreshEntranceUI',RefreshEntranceUI)
util.hotfix_ex(CS.SpecialMissionInfoController,'RefresCommonUI',RefresCommonUI)
util.hotfix_ex(CS.SpecialMissionInfoController,'GotoDeployment',GotoDeployment)
util.hotfix_ex(CS.SpecialMissionInfoController,'RequestStartMissionHandle',RequestStartMissionHandle)
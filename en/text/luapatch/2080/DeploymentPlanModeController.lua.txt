local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentPlanModeController)
xlua.private_accessible(CS.DeploymentController)
local UpdateStatus = function(self)
	if self.ClickSpotEvent == nil then
		return;
	end
	self:UpdateStatus();
end

local Init = function(self)
	if CS.GameData.missionResult ~= nil then
		if CS.GameData.missionAction == nil then
			CS.GameData.missionResult = nil;
		end
	end
	self:Init();
end

local _CancelPlan = function(self)
	if CS.DeploymentPlanModeController.Instance.status == CS.DeploymentPlanModeController.PlanStatus.pause then
		print("cancel")
		CS.DeploymentController.Instance:AddAndPlayPerformance(nil);
	end
	self:_CancelPlan();
	if CS.DeploymentController.Instance.engagedSpot ~= nil then
		CS.DeploymentController.TriggerSwitchAbovePanelEvent(true);
	end
end
local Update = function(self)
	if CS.DeploymentController.Instance ~= nil then
		if CS.DeploymentController.Instance._randomEventController ~= nil and not CS.DeploymentController.Instance._randomEventController:isNull() then
			if CS.DeploymentController.Instance._randomEventController.gameObject.activeSelf then				
				return;
			end
		end
	end
	self:Update();
end
util.hotfix_ex(CS.DeploymentPlanModeController,'UpdateStatus',UpdateStatus)
util.hotfix_ex(CS.DeploymentPlanModeController,'Init',Init)
util.hotfix_ex(CS.DeploymentPlanModeController,'_CancelPlan',_CancelPlan)
util.hotfix_ex(CS.DeploymentPlanModeController,'Update',Update)


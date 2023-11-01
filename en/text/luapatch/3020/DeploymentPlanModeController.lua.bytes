local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentPlanModeController)
xlua.private_accessible(CS.DeploymentPlanModeController.Plan)
--修正计划移动线层级
local CheckData = function(self)
	if CS.DeploymentBackgroundController.currentLayerData == nil then
		local layer = CS.DeploymentBackgroundController.currentlayer;
		CS.DeploymentBackgroundController.currentLayerData = CS.DeploymentBackgroundController.layerDatas[layer];
	end
	self:CheckData();
end

util.hotfix_ex(CS.DeploymentPlanModeController,'CheckData',CheckData)



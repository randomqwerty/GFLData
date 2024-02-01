local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentPlanModeController)

local UpdateApText = function(self)
	if CS.DeploymentController.Instance ~= nil and not CS.DeploymentController.Instance:isNull() then
		self:UpdateApText();
	end
end

util.hotfix_ex(CS.DeploymentPlanModeController,'UpdateApText',UpdateApText)

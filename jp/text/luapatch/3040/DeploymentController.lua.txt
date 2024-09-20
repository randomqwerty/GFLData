local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentPlanModeController)
xlua.private_accessible(CS.DeploymentController)
local UpdateApText = function(self)
	if CS.DeploymentController.Instance ~= nil and not CS.DeploymentController.Instance:isNull() then
		self:UpdateApText();
	end
end

local cantransfer = function(skill,spot)
	if spot.spotAction.HasTeam then
		return false;
	end
	return CS.DeploymentController.cantransfer(skill,spot);
end
local HasCombination = function(self)
	return CS.GuideManagerController.Instance == nil and self:HasCombination()
end
util.hotfix_ex(CS.DeploymentPlanModeController,'UpdateApText',UpdateApText)
--util.hotfix_ex(CS.DeploymentController,'cantransfer',cantransfer)
util.hotfix_ex(CS.DeploymentController,'HasCombination',HasCombination)
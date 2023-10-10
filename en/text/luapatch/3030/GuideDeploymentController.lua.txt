local util = require 'xlua.util'
xlua.private_accessible(CS.GuideDeploymentController)

local ClearGuideData = function()	
	CS.GuideDeploymentController.ClearGuideData();
	if CS.DeploymentController.isDeplyment then
		CS.GuideDeploymentController.currentMissionGuideData = nil;
	end
end

util.hotfix_ex(CS.GuideDeploymentController,'ClearGuideData',ClearGuideData)


local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentController)

local RequestStartMissionHandle = function(self,json)
	self:RequestStartMissionHandle(json);
	CS.DeploymentUIController.Instance:RefreshUI();
end


util.hotfix_ex(CS.DeploymentController,'RequestStartMissionHandle',RequestStartMissionHandle)

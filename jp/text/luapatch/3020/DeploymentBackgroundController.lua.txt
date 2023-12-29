local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBackgroundController)
xlua.private_accessible(CS.DeploymentController)

local TriggerInitEvent = function()
	
end
local RequestMissionCombinationHandle = function(self,data)
	self:RequestMissionCombinationHandle(data);
	CS.DeploymentController.Instance:InitField();
end

util.hotfix_ex(CS.DeploymentController,'TriggerInitEvent',TriggerInitEvent)
util.hotfix_ex(CS.DeploymentBackgroundController,'RequestMissionCombinationHandle',RequestMissionCombinationHandle)


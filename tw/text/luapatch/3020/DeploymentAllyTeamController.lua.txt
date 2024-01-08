local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentAllyTeamController)

local ClearBuffUI = function(self)

end
local allyTeamInstanceId = function(self)
	if self.allyTeam ~= nil then
		return self.allyTeam.instanceId;
	else
		return self.allyinstanceid;
	end
end
util.hotfix_ex(CS.DeploymentAllyTeamController,'ClearBuffUI',ClearBuffUI)
util.hotfix_ex(CS.DeploymentAllyTeamController,'get_allyTeamInstanceId',allyTeamInstanceId)
local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamController)

local Start = function(self)
	self:Start()
	self:RefeshBuffUI();
end

util.hotfix_ex(CS.DeploymentTeamController,'Start',Start)




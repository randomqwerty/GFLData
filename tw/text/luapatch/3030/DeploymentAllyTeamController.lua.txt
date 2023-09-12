local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentAllyTeamController)

local ClearBuffUI = function(self)

end
util.hotfix_ex(CS.DeploymentAllyTeamController,'ClearBuffUI',ClearBuffUI)
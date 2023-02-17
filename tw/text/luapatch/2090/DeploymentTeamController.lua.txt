local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamController)

local allFreeBuffMreAmmo = function(self)
	return false;
end

util.hotfix_ex(CS.DeploymentTeamController,'allFreeBuffMreAmmo',allFreeBuffMreAmmo)
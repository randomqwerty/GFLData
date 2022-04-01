local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamController)

local Start = function(self)
	self:Start()
	self:RefeshBuffUI();
end

local allFreeBuffMreAmmo = function(self)
	return false;
end
util.hotfix_ex(CS.DeploymentTeamController,'Start',Start)
util.hotfix_ex(CS.DeploymentTeamController,'allFreeBuffMreAmmo',allFreeBuffMreAmmo)




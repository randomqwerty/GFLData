local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamController)
xlua.private_accessible(CS.DeploymentMapDragController)

local TransferComplete = function(self)
	self:TransferComplete();
	self:RefreshTeamInfo();
end

local allFreeBuffMreAmmo = function(self)
	return false;
end

util.hotfix_ex(CS.DeploymentTeamController,'TransferComplete',TransferComplete)
util.hotfix_ex(CS.DeploymentTeamController,'allFreeBuffMreAmmo',allFreeBuffMreAmmo)


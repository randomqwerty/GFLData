local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBuildingController)

local InitCode = function(self,code)
	if self.buildname ~= code then
		self.mat = nil;
	end
	self:InitCode(code);
end
util.hotfix_ex(CS.DeploymentBuildingController,'InitCode',InitCode)

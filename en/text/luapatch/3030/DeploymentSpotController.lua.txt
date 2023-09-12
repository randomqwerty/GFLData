local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentSpotController)

local Checkroute = function(self)
	if self.spotInfo == nil then
		return;
	end
	self:Checkroute();
end

util.hotfix_ex(CS.DeploymentSpotController,'Checkroute',Checkroute)
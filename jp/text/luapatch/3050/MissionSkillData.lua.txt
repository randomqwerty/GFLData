local util = require 'xlua.util'

local deploymentTeam = function(self)
	self._deploymentTeam = nil;
	return self.deploymentTeam;
end

util.hotfix_ex(CS.BuffAction,'get_deploymentTeam',deploymentTeam)

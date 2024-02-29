local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentSpotController)


local CurrentTeamEchelon = function(self)
	if self.currentTeam ~= nil and not self.currentTeam:isNull() then
		return self.currentTeam:PersonType();
	end
	return 0;
end

util.hotfix_ex(CS.DeploymentSpotController,'CurrentTeamEchelon',CurrentTeamEchelon)
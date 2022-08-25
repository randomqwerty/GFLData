local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamController)

local Fade = function(self)
	self:Fade();
	if self.currentSpot.currentTeam == self and self.currentSpot.currentTeamTemp ~= nil then
		self.currentSpot.currentTeam = self.currentSpot.currentTeamTemp;
		self.currentSpot.currentTeamTemp = nil;
	end
end

local Die = function(self)
	self:Die();
	if self.currentSpot.currentTeam == self and self.currentSpot.currentTeamTemp ~= nil then
		self.currentSpot.currentTeam = self.currentSpot.currentTeamTemp;
		self.currentSpot.currentTeamTemp = nil;
	end
end
util.hotfix_ex(CS.DeploymentTeamController,'Fade',Fade)
util.hotfix_ex(CS.DeploymentTeamController,'Die',Die)
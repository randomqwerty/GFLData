local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentSquadTeamController)

local CheckBattleSkill = function(self)
	self.squadTeam.currentSpotInfo = self.currentSpot.spotInfo;
	self:CheckBattleSkill();
end

util.hotfix_ex(CS.DeploymentSquadTeamController,'CheckBattleSkill',CheckBattleSkill)


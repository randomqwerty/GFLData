local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentAllyTeamController)

local RefreshTeam = function(self)
	if self.allyTeam.currentBelong ~= CS.TeamBelong.friendly then
		local enemyTeamInfo = CS.GameData.listEnemyTeamInfo:GetDataById(self.allyTeam.EnemyTeamId);
		local typeInfo = CS.GameData.listEnemyCharacterTypeInfo:GetDataById(enemyTeamInfo.enemyLeaderId);
		if self.leaderCode ~= typeInfo.code then
			self.mRecordItem:Clear();
			self:AnalysicsDropData();
		end
	end
	self:RefreshTeam();
end

--util.hotfix_ex(CS.DeploymentAllyTeamController,'RefreshTeam',RefreshTeam)




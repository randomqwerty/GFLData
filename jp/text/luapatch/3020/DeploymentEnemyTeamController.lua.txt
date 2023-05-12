local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentEnemyTeamController)

local get_EnemyTeamPower = function(self)
	if self.enemyTeamInfo ~= nil and self.enemyTeamInfo.effect_ext ~= 0 then
		if self.enemyTeamInfo.effect_ext>0 then
			return self.enemyTeamInfo.effect_ext;
		else
			if self.enemyGuns.Count == 0 then
				return 0;	
			end
			if self.isBoss and self.bossMaxHP == 0 then
				return 0;
			end
			return self.EnemyTeamPower;
		end
	end
	return self.RealTeamPower;
end

util.hotfix_ex(CS.DeploymentEnemyTeamController,'get_EnemyTeamPower',get_EnemyTeamPower)

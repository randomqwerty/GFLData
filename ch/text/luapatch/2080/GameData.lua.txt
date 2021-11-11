local util = require 'xlua.util'
xlua.private_accessible(CS.SpotAction)

local EnemyDataClear = function(self)
	self:EnemyDataClear();
	self.enemyTeamId = 0;
end

util.hotfix_ex(CS.SpotAction,'EnemyDataClear',EnemyDataClear)



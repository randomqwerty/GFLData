local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleCharacterController)
xlua.private_accessible(CS.GF.Battle.SkillUtils)
local DeathClear = function(self)

	self:DeathClear()
	CS.GF.Battle.SkillUtils.sSortScout:Clear()
end

util.hotfix_ex(CS.GF.Battle.BattleCharacterController,'DeathClear',DeathClear)
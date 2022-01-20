local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleController)

local CheckSkillCD = function(self)
	self:CheckSkillCD()
	if not self.ifEnemyDie then
		CS.GF.Battle.SkillUtils.GetSkillCDInfo()
	end
end

util.hotfix_ex(CS.GF.Battle.BattleController,'CheckSkillCD',CheckSkillCD)


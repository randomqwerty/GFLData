local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleCharacterData)
local UpdateLife = function(self,damageInfo,damage)
	if self.conditionListSelf:Exists(CS.CharacterConditionType.shallowgrave) then
		local trueDamage = -damage
		local t = (self.currentLife - damage) % self.memberLife
		local memberAfterDamage = (self.currentLife - trueDamage) / self.memberLife
		if t ~= 0 then
			memberAfterDamage = memberAfterDamage + 1
		end
		if memberAfterDamage < self.memberCount then
			trueDamage = self.currentLife - (self.memberLife * (self.memberCount -1) + 1)
			damage = - trueDamage
		end
	end
	self:UpdateLife(damageInfo,damage)

end

util.hotfix_ex(CS.GF.Battle.BattleCharacterData,'UpdateLife',UpdateLife)
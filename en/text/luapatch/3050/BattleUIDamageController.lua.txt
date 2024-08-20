local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleManager)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)
xlua.private_accessible(CS.BattleUIDamageController)

local ShowDamageText = function(self,position,damage,isCrit,isMiss,isAbsorb,defPercent,adType,immuneType)
	local active = CS.BattleSangvisSpecialSkillController.Instance.isSpecialSkillActive
	self:ShowDamageText(position,damage,isCrit,isMiss,isAbsorb,defPercent,adType,immuneType)
	if active then
		self.damageText.gameObject:SetLayerRecursively(5)
	end

end
local Init = function(self)
	self:Init()
	if CS.GF.Battle.BattleDynamicData.isSangvisBattle then
		self.gameObject.layer = 5
		util.hotfix_ex(CS.BattleUIDamageController,'ShowDamageText',ShowDamageText)
	else
		xlua.hotfix(CS.BattleUIDamageController,'ShowDamageText',nil)
	end
end

util.hotfix_ex(CS.BattleUIDamageController,'Init',Init)

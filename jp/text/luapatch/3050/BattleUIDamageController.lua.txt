local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleManager)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)
xlua.private_accessible(CS.BattleUIDamageController)
xlua.private_accessible(CS.BattleSkillTipItem)

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
local InitData = function(self,skillType,desc)
	self.txtDesc.isOrnamental = false;
	self:InitData(skillType,desc);
	self.txtDesc.gameObject:SetActive(true);
end
util.hotfix_ex(CS.BattleUIDamageController,'Init',Init)
util.hotfix_ex(CS.BattleSkillTipItem,'InitData',InitData)

local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleCharacterControllerNew)
xlua.private_accessible(CS.GF.Battle.BattleCharacterData)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)
xlua.private_accessible(CS.BattleUILifeBarController)
local FP = CS.TrueSync.FP
local TryShowLifeBar = function(self)

	if self.mCharacter ~= nil and self.mCharacter.isDead then
		return
	end
	if self.showLifeBar then
		self.gameObject:SetActive(true)
	end
end

xlua.hotfix(CS.BattleUILifeBarController,'TryShowLifeBar',TryShowLifeBar)

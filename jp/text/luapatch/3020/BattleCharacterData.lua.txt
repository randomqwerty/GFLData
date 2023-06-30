local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleCharacterData)
local FP = CS.TrueSync.FP
local InitSpecialAttribute = function(self,code)
	if self.isEnemy and code == "Jaguar" then
		self.gun.number = 1		
	end
	self:InitSpecialAttribute(code)
end
local GetEnemyData = function(self)
	self:GetEnemyData()
	self.gunLife = FP.FromFloat(self.gun.life)
end
util.hotfix_ex(CS.GF.Battle.BattleCharacterData,'InitSpecialAttribute',InitSpecialAttribute)
util.hotfix_ex(CS.GF.Battle.BattleCharacterData,'GetEnemyData',GetEnemyData)
local util = require 'xlua.util'
xlua.private_accessible(CS.BattleEnemyCharacterController)
local flatSkillCancelFlag = false
local flatSkillCancelCounter = 0
local SLGScout = function(self)
	if self.status == CS.GF.Battle.CharacterStatus.advancing then
		if self.transform.localPosition ~= self.nextPos then
			return 
		end
	end
	self.mCommonTarget = nil
	self:SLGScout()
end

util.hotfix_ex(CS.BattleEnemyCharacterController,'SLGScout',SLGScout)


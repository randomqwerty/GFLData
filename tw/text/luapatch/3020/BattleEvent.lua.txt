local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleCharacterAnimatorEvent)

local BattleCharacterAnimatorEvent = function(self,data,name,type)
	self.characterData = data
	self.animName = name
end

util.hotfix_ex(CS.GF.Battle.BattleCharacterAnimatorEvent,'.ctor',BattleCharacterAnimatorEvent)
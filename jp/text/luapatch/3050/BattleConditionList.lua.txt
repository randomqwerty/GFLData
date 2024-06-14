local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleConditionList)


local BattleConditionList = function(self,data)
	self.useNewExist = false
end


util.hotfix_ex(CS.GF.Battle.BattleConditionList,'.ctor',BattleConditionList)
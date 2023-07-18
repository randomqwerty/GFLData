local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.CharacterCondition)
local FP = CS.TrueSync.FP
local Power = function(self,value,num)
	local valueF = value:AsFloat()
	return FP.FromFloat(valueF ^ num)
end

xlua.hotfix(CS.GF.Battle.CharacterCondition,'Power',Power)
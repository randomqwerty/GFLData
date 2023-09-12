local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleMemberManager)
xlua.private_accessible(CS.GF.Battle.BattleMemberData)
xlua.private_accessible(CS.GF.Battle.BattleCharacterManager)
xlua.private_accessible(CS.GF.Battle.BattleFriendlyCharacterManager)
xlua.private_accessible(CS.GF.Battle.BattleCharacterData)

local FP = CS.TrueSync.FP

local VectorEquals = function(self,a,b,min)
	local varDistance = (self.realtimeSpeed:AsFloat()) *  0.2 / 30
	local distance = (varDistance + (CS.TrueSync.TSVector.Distance(self.data.characterPosition,self.data.startPosition):AsFloat())) / self.data.switchDistance:AsFloat()
	return distance >= 1
	
end
local OnReceiveAdvanceEvent = function(self,obj,e)
	if self.isDeadOrRetreat then
		return 
	end
	if self.data.isSquad then
		return 
	end
	self:SetCharacterStatus(CS.GF.Battle.CharacterStatus.advancing)
	self:Scout()
end



xlua.hotfix(CS.GF.Battle.BattleFriendlyCharacterManager,'VectorEquals',VectorEquals)
xlua.hotfix(CS.GF.Battle.BattleFriendlyCharacterManager,'OnReceiveAdvanceEvent',OnReceiveAdvanceEvent)
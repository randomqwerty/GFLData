local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleMemberManager)
xlua.private_accessible(CS.GF.Battle.BattleMemberData)
xlua.private_accessible(CS.GF.Battle.BattleCharacterManager)
xlua.private_accessible(CS.GF.Battle.BattleEventManager)
xlua.private_accessible(CS.GF.Battle.BattleCharacterData)


local UpdateSpineStatus = function(self,priority,animSpeed)
	if self.data.spineAnimationSourceLevel > priority then
		
	else
		self:UpdateSpineStatus(priority,animSpeed)
	end
	
	
end
local SetSpineAnimation = function(self,name,priority,animSpeed,isLoop)
	self:SetSpineAnimation(name,priority,animSpeed,isLoop)
	self.data.curDir = self.data.selfDir
	self.data.spineTimeScale = animSpeed
	self.data.needUpdateSpine = true
end

local GetSelfPos = function(self,isformoffset)
	if isformoffset then
		return self.data.parentData:GetWorldPos()
	else
		return self.data:GetWorldPos()
	end
end


util.hotfix_ex(CS.GF.Battle.BattleMemberManager,'UpdateSpineStatus',UpdateSpineStatus)
util.hotfix_ex(CS.GF.Battle.BattleMemberManager,'SetSpineAnimation',SetSpineAnimation)
--xlua.hotfix(CS.GF.Battle.BattleMemberManager,'GetSelfPos',GetSelfPos)
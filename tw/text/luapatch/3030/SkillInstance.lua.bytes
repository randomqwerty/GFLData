local util = require 'xlua.util'

xlua.private_accessible(CS.GF.Battle.CSkillInstance)
xlua.private_accessible(CS.GF.Battle.CharacterSkillImpl)

local FP = CS.TrueSync.FP
local Play = function(self,bTurnToDes)
	self:Play(bTurnToDes)
	if not self.mFinish then
		if self.mTargets.Count > 0 then
			self.mTargets[0].defPos = self.mTargets[0]:GetPos()
		end
	end
end
local _HandleScrEffectEvent = function(self,pEvent)
	
	if pEvent.ID == 5 or pEvent.ID == 8 then
		if self.mTargets.Count > 0 then
			self.mTargetPoses:Add(self.mTargets[0].defPos)
		end
	end
	self:_HandleScrEffectEvent(pEvent)
	if pEvent.ID == 5 or pEvent.ID == 8 then
		self.mTargetPoses:Clear()
	end
end
--在battlecontroller
--util.hotfix_ex(CS.GF.Battle.CSkillInstance,'Play',Play)
--util.hotfix_ex(CS.GF.Battle.CSkillInstance,'_HandleScrEffectEvent',_HandleScrEffectEvent)

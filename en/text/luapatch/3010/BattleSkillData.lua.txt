local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleSkillData)
local UpdateCD = function(self)	
	self:UpdateCD()
	if self.cdChargeIntervalFrame > 0 then		
		self.cdChargeIntervalFrame = self.cdChargeIntervalFrame - 1
	end
	if not self.isStartingCD and  self.isChargeSkill and self.currentChargeTier >= self.MaxChargeTier then
		self:SetSkillCD(self.cdFrame + 1)
	end
	if not self.isStartingCD and self.cdFrame == 0 then		
		self:OnCDComplete()
	end	
end


util.hotfix_ex(CS.GF.Battle.BattleSkillData,'UpdateCD',UpdateCD)
local util = require 'xlua.util'
local added = false
xlua.private_accessible(CS.GF.Battle.Gun)
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
local CreateFriendlyCharacter = function(self,skill)	
	self:CreateFriendlyCharacter(skill)
	local flag = false
	for i=0,self.listFriendlyGun.Count-1 do
		local gun = self.listFriendlyGun[i]
		if gun ~= nil and gun.life >0 then			
			for j=0,gun.mVecSkill.Count-1 do
				local skill = gun.mVecSkill[j]
				if skill ~= nil and skill.info ~= nil then
					if skill.info.isChargeCDSkill then
						flag = true							
						break
					end
				end
			end			
		end
		if flag == true then
			break
		end
	
	end
	if flag == true then
		xlua.private_accessible(CS.GF.Battle.BattleSkillData)
		util.hotfix_ex(CS.GF.Battle.BattleSkillData,'UpdateCD',UpdateCD)	
	else
		xlua.hotfix(CS.GF.Battle.BattleSkillData,'UpdateCD',nil)
	end
end
util.hotfix_ex(CS.GF.Battle.BattleController,'CreateFriendlyCharacter',CreateFriendlyCharacter)	


local util = require 'xlua.util'
xlua.private_accessible(CS.Vehicle)

local GetComponentExtraSkills = function(self)

	self:GetComponentExtraSkills()
	for i=0,self.listOriginalComponents.Count-1 do
		if not self.listOriginalComponents[i]:IsBattleComponent() then
			if self.listOriginalComponents[i].info.componentMainSkill ~= nil then
				self.listOriginalComponents[i].info.componentMainSkill.isManual = self.listOriginalComponents[i].forceManualSkill
			end
		end
	end
end

util.hotfix_ex(CS.Vehicle,'GetComponentExtraSkills',GetComponentExtraSkills)



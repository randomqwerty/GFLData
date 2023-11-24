local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleController)
xlua.private_accessible(CS.GF.Battle.BattleCharacterData)
local ShowSkillPerformance= function(self,obj,e)
	self:ShowSkillPerformance(obj,e)
	if e.data.isFriendly then
		local character = self:GetControllerByData(e.data)
		if character ~= nil then
			character:PlaySkillVoice()
		end
	end
end

util.hotfix_ex(CS.GF.Battle.BattleController,'ShowSkillPerformance',ShowSkillPerformance)

local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleController)
local IsSangvisSkillPerformanceOn = function(id)
	local t = CS.GF.Battle.BattleController.Instance
	if t ~= nil and t.isTheaterPerform then
		return false
	end
	return CS.ConfigData.IsSangvisSkillPerformanceOn(id)
end

util.hotfix_ex(CS.ConfigData,'IsSangvisSkillPerformanceOn',IsSangvisSkillPerformanceOn)
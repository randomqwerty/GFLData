local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleController)

local TriggerPerformance = function(self,scene)
	local t = CS.GF.Battle.BattleController.Instance
	if t ~= nil and t.isTheaterPerform then
		return
	end
	self:TriggerPerformance(scene)
end
util.hotfix_ex(CS.BattleChangeBackgroundPerformanceController,'TriggerPerformance',TriggerPerformance)
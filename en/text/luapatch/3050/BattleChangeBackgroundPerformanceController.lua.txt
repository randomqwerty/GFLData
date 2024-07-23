local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleManager)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)
xlua.private_accessible(CS.GF.Battle.BattleController)
xlua.private_accessible(CS.BattleChangeBackgroundPerformanceController)

local TriggerPerformance = function(self,scene)
	if CS.GameData.engagedSpot ~= nil and 
		(   CS.GameData.engagedSpot.enemyTeamId == 9700301 or 
			CS.GameData.engagedSpot.enemyTeamId == 9701901 or
			CS.GameData.engagedSpot.enemyTeamId == 9701201 or
			CS.GameData.engagedSpot.enemyTeamId == 9702201 or
			CS.GameData.engagedSpot.enemyTeamId == 9701501 or
			CS.GameData.engagedSpot.enemyTeamId == 9702301)then
		scene.code = CS.GF.Battle.BattleController.Instance.background.code
	end
	self:TriggerPerformance(scene)
end

util.hotfix_ex(CS.BattleChangeBackgroundPerformanceController,'TriggerPerformance',TriggerPerformance)

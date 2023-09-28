local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleController)
xlua.private_accessible(CS.GF.Battle.BattleCharacterData)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)
xlua.private_accessible(CS.GF.Battle.BattleManager)
local FP = CS.TrueSync.FP


local CalcRemoteBattleEnemyRemainPercent= function(self)
	local listEnemyCharacterData = CS.GF.Battle.BattleDynamicData.listEnemyCharacterData
	for i = 0,listEnemyCharacterData.Count - 1 do
		local data = listEnemyCharacterData[i]
		data.bulletChainNum = data.startingLife
		data.startingLife = data.maxLife
		
	end
	
	self:CalcRemoteBattleEnemyRemainPercent()
	
	for i = 0,listEnemyCharacterData.Count - 1 do
		local data = listEnemyCharacterData[i]
		data.startingLife = data.bulletChainNum
		
	end
	local BattleDynamicData = CS.GF.Battle.BattleDynamicData
	if BattleDynamicData.enemyAllyTeam ~= nil then
		if BattleDynamicData.enemyAllyTeam.hpPercent <= 0 then
			BattleDynamicData.enemyAllyTeam.hpPercent = 0
		end
	else
		if BattleDynamicData.enemyTeamData ~= nil then
			if BattleDynamicData.enemyTeamData.hpPercent <= 0 then
				BattleDynamicData.enemyTeamData.hpPercent = 0
			end
		end
	end
	
end


util.hotfix_ex(CS.GF.Battle.BattleManager,'CalcRemoteBattleEnemyRemainPercent',CalcRemoteBattleEnemyRemainPercent)
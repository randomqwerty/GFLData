local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleController)
xlua.private_accessible(CS.GF.Battle.BattleCharacterData)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)
xlua.private_accessible(CS.GF.Battle.BattleManager)



local CalcRemoteBattleEnemyRemainPercent= function(self)
	self:CalcRemoteBattleEnemyRemainPercent()
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
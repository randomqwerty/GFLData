local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)
xlua.private_accessible(CS.GF.Battle.BattleReplayController)
local TurnLevelCorrect = function(self)	
	if CS.GF.Battle.BattleDynamicData.isReplayMode then
		local turn = CS.GF.Battle.BattleReplayController.repData.currentTurn;
		if turn<0 then
			return 0;
		end
		local addlevel = 0;
		for i=0,self.turncorrect.Count-1 do
			if turn>=self.turncorrect[i] then
				addlevel = self.levelcorrect[i];
			end 
		end
		return addlevel;
	end
	if CS.GameData.missionAction == nil then
		return 0;
	else
		local addlevel = 0;
		for i=0,self.turncorrect.Count-1 do
			if CS.GameData.missionAction.turn>=self.turncorrect[i] then
				addlevel = self.levelcorrect[i];
			end
		end
		return addlevel;
	end
end


util.hotfix_ex(CS.EnemyTeamInfo,'get_TurnLevelCorrect',TurnLevelCorrect)
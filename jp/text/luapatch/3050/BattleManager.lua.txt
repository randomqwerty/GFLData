local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleManager)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)

local RequestBattleFinish = function(self,forceLose)
	local isBattleFinished = CS.GF.Battle.BattleDynamicData.isBattleFinished
	
	--print("isBattleFinished")
	--print(CS.GF.Battle.BattleDynamicData.EntranceType)
	
	self:RequestBattleFinish(forceLose)
	if isBattleFinished then
		
		if CS.GF.Battle.BattleDynamicData.EntranceType == CS.BattleEntranceType.SLGMiniGame then
			CS.GF.Battle.BattleController.Instance:RequestBattleFinish()
		end
	end
end

util.hotfix_ex(CS.GF.Battle.BattleManager,'RequestBattleFinish',RequestBattleFinish)
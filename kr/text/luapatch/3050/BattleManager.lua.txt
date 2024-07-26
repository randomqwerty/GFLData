local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleManager)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)
xlua.private_accessible(CS.GF.Battle.BattleFieldTeamHolderNew)

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
local CheckIsSLGMode = function()
	if CS.GameData.engagedSpot ~= nil and CS.GameData.engagedSpot.enemyTeamId >= 513701 and CS.GameData.engagedSpot.enemyTeamId <= 513704 then
		return true
	end
	return false
end
local CheckAllIsPhased= function(self,listBattleCharacterController)
	if listBattleCharacterController:Equals(CS.GF.Battle.BattleDynamicData.friendlyTeamHolder.listCharacter) then
		local resultValue = self:CheckAllIsPhased(listBattleCharacterController)
		if resultValue then
			for i=0,listBattleCharacterController.Count-1 do
				if listBattleCharacterController[i].data:ExistsBuff(5297,1) then
					return false
				end
			end
			return true
		else
			return resultValue
		end
	else
		return self:CheckAllIsPhased(listBattleCharacterController)
	end
end
util.hotfix_ex(CS.GF.Battle.BattleManager,'RequestBattleFinish',RequestBattleFinish)
util.hotfix_ex(CS.GF.Battle.BattleManager,'CheckAllIsPhased',CheckAllIsPhased)
util.hotfix_ex(CS.GF.Battle.BattleDynamicData,'CheckIsSLGMode',CheckIsSLGMode)
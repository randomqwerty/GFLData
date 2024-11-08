local util = require 'xlua.util'
xlua.private_accessible(CS.BreakoutAVGController)

local TriggerAVG = function(self,missionId,phaseOrder,triggerType,parent)
	local phaseId = CS.GF.Tarkov.GameDataCache.I.playerData.phaseId
	if triggerType == CS.BreakoutAVGController.AVGTriggerType.BattleEnd then
		local list = CS.GF.Tarkov.GameDataCache.I.listPhaseInfo
        local length = list.Count-1
		for i=0, length do
			local phase = list:GetDataByIndex(i);
			if phase.mission == missionId and phase.order == phaseOrder then
				CS.GF.Tarkov.GameDataCache.I.playerData.phaseId = phase.id
				break
			end	
		end
		list = nil
	end
	local result = self:TriggerAVG(missionId,phaseOrder,triggerType,parent)
	CS.GF.Tarkov.GameDataCache.I.playerData.phaseId = phaseId
	return result
end

util.hotfix_ex(CS.BreakoutAVGController,'TriggerAVG',TriggerAVG)





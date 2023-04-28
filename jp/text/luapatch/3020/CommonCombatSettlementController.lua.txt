local util = require 'xlua.util'
xlua.private_accessible(CS.CommonCombatSettlementController)

local Start = function(self)
	self:Start();
	if not self.isAutoMission then
		local mission = CS.GameData.listMission:GetDataById(CS.GameData.currentSelectedMissionInfo.id);
		if CS.GameData.missionResult ~= nil then
			if CS.GameData.missionResult.rank ~= CS.Rank.C and CS.GameData.missionResult.rank ~= CS.Rank.D then
				mission.medal1 = true;
			end
			if not mission.medal2 then
				mission.medal2 = CS.GameData.missionResult.medal4;
			end
		end
	end
end
util.hotfix_ex(CS.CommonCombatSettlementController,'Start',Start)
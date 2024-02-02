local util = require 'xlua.util'
xlua.private_accessible(CS.AVGPlayBackInfo)

local mission = function(self)
	if self.campaign < 0 then
		for i=0,self.listMissionInfo.Count-1 do
			local mission = CS.Data.FromMissionInfoSelectMission(self.listMissionInfo[i]);
			if mission ~= nil then
				if mission.missionInfo.isEndless then
					return mission;
				elseif mission.eventprize ~= nil and mission.winCount >= mission.eventprize.bossHpBars then
					return mission;
				end
			end
		end
		return nil;
	end
	return self.mission;
end

util.hotfix_ex(CS.AVGPlayBackInfo,'get_mission',mission)

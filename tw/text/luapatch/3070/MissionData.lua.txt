local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSkipInfo)

local Percent = function(self)
	local num = 0;
	local allnum = 0;
	for i=0,self.checkMissions.Count-1 do
		local missionInfo = CS.GameData.listMissionInfo:GetDataById(self.checkMissions[i]);
		local mission = CS.GameData.listMission:GetDataById(self.checkMissions[i]);
		local isNightMission = missionInfo.specialType == CS.MapSpecialType.Night;
		if isNightMission then
			allnum = allnum +1;
			if mission ~= nil and mission.bestRank ~= CS.Rank.C and mission.bestRank ~= CS.Rank.D then
				num = num +1;
			end
		else
			allnum = allnum +3;
			if mission ~= nil then
				if mission.bestRank ~= CS.Rank.C and mission.bestRank ~= CS.Rank.D then
					num = num +1;
				end
				if mission.medal2 then
					num = num +1;
				end
				if mission.bestRank == CS.Rank.S then
					num = num +1;
				end
			end
		end
	end
	return num/allnum;
end
util.hotfix_ex(CS.MissionSkipInfo,'Percent',Percent)

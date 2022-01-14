local util = require 'xlua.util'
xlua.private_accessible(CS.BuildingAction)

local AddDieEnemyCount = function(self,enemyteam,addnum)
	self:AddDieEnemyCount(enemyteam,addnum);
	self.allDieEnemyNum = self.allDieEnemyNum + addnum;
end

local UseWinCounter = function(self)
	if self.missionInfo.mapped_mission_id ~= 0 then
		local mapInfo = CS.GameData.listMissionMapInfo:GetDataById(self.missionInfo.mapped_mission_id);
		if 	mapInfo == nil then
			return self.winCount;
		end
		local missionids = mapInfo.missionids;
		local index = missionids:IndexOf(self.missionInfo.id);
		if index == 1 or index == 2 then
			if self.winCount>0 and self.mappedwincounter>0 then
				return self.mappedwincounter;
			else
				return 0;
			end
		elseif index == 0 then
			if self.mappedwincounter>0 then
				return self.mappedwincounter;
			else
				return self.winCount;
			end
		end
	end
	return self.winCount;
end
util.hotfix_ex(CS.MissionAction,'AddDieEnemyCount',AddDieEnemyCount)
util.hotfix_ex(CS.Mission,'get_UseWinCounter',UseWinCounter)
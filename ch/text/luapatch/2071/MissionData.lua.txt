local util = require 'xlua.util'
xlua.private_accessible(CS.Mission)

local UseWinCounter = function(self)
	if self.missionInfo.mapped_mission_id ~= 0 then		
		local missionids = CS.GameData.listMissionMapInfo:GetDataById(self.missionInfo.mapped_mission_id).missionids;
		local index = missionids:IndexOf(self.missionInfo.id);
		if index==1 then
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

util.hotfix_ex(CS.Mission,'get_UseWinCounter',UseWinCounter)
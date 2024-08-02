local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionMissionDetailController)
xlua.private_accessible(CS.MissionSelectionEchelonController)
local mGetRaidLimit = function(self)
	self:GetRaidLimit();
	local limitRaid = CS.Data.GetInt("simulate_sweeping_maxnum",0);
	if self._tmpRaidLimit > limitRaid then 
		--local c = self._tmpRaidLimit-limitRaid;
		--print("超了"..c);
		self._tmpRaidLimit=limitRaid;
    end
    return self._tmpRaidLimit;
end

local ShowTeamInfo = function(self,Id)
	if self.selectionType == 0 then
		local count = CS.GameData.userInfo.maxTeam;
		CS.GameData.userInfo.maxTeam = count + 1;
		self:ShowTeamInfo(Id);
		CS.GameData.userInfo.maxTeam = count;
	else
		self:ShowTeamInfo(Id);
	end
end
util.hotfix_ex(CS.MissionSelectionMissionDetailController,'GetRaidLimit',mGetRaidLimit)
util.hotfix_ex(CS.MissionSelectionEchelonController,'ShowTeamInfo',ShowTeamInfo)

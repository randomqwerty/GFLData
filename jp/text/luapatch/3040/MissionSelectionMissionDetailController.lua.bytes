local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionMissionDetailController)

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

util.hotfix_ex(CS.MissionSelectionMissionDetailController,'GetRaidLimit',mGetRaidLimit)

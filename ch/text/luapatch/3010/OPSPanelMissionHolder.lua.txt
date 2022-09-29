local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMissionHolder)

local AllCount = function(self)
	if self.groupInfo ~= nil then
		return  self.groupInfo.missionids.Count;
	end
	if self.opsMission ~= nil then
		return  self.opsMission:AllCount();
	end
	return 0;
end

util.hotfix_ex(CS.OPSPanelMissionHolder,'AllCount',AllCount)





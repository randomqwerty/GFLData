local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMissionHolder)

local CanShow = function(self)
	if self.opsMission ~= nil and self.opsMission.entranceId == 0 and self.spots3D.Count == 0 then
		return self.opsMission.currentMission ~= nil;
	end
	return self.CanShow;
end

util.hotfix_ex(CS.OPSPanelMissionHolder,'get_CanShow',CanShow)






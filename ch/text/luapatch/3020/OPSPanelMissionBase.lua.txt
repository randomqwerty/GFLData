local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMissionBase)

local currentMission = function(self)
	if self.opsMission ~= nil then
		return self.opsMission.currentMission;	
	end
	return self.currentMission;
end
util.hotfix_ex(CS.OPSPanelMissionBase,'get_currentMission',currentMission)





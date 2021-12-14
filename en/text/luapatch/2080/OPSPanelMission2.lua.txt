local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMission2)

local ShowSelf = function(self)
	if self.currentMission == nil then
		return;
	end
	self:ShowSelf();
end


util.hotfix_ex(CS.OPSPanelMission2,'ShowSelf',ShowSelf)



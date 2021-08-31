local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMissionBase)

local PlayShow = function(self)
	self.lastmissioninfo = nil;
	self:PlayShow();
end

util.hotfix_ex(CS.OPSPanelMissionBase,'PlayShow',PlayShow)



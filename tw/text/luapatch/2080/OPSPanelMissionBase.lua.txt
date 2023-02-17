local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMissionBase)

local PlayShow = function(self)
	self.lastmissioninfo = nil;
	self:PlayShow();
end

local CheckDropMissionkeyInfo = function(self,txt)
	if self.currentMission == nil then
		return;
	end
	self:CheckDropMissionkeyInfo(txt);
end

util.hotfix_ex(CS.OPSPanelMissionBase,'PlayShow',PlayShow)
util.hotfix_ex(CS.OPSPanelMissionBase,'CheckDropMissionkeyInfo',CheckDropMissionkeyInfo)


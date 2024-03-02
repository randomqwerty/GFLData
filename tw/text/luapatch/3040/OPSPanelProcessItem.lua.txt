local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelProcessItem)

local RefreshUI = function(self)
	if self.info.panelHolder ~= nil then
		self.info.diffcluty = self.info.opsMission.missionIds:IndexOf(self.info.mission.missionInfo.id);
	end
	self:RefreshUI();
end

util.hotfix_ex(CS.OPSPanelProcessItem,'RefreshUI',RefreshUI)


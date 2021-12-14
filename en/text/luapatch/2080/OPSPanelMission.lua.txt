local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMission)

local Click = function(self)
	if self.holder.containerId ~= CS.OPSPanelBackGround.currentContainerId then
		 return;
	end
	self:Click();
end

util.hotfix_ex(CS.OPSPanelMission,'Click',Click)



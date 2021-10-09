local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelMissionHolder)

local CanShow = function(self)
	if self.containerId ~= CS.OPSPanelBackGround.currentContainerId then
		 return false;
	end
	return self.CanShow;
end

local PlayMove = function(self)
	CS.OPSPanelBackGround.Instance:CheckShowMoveOffset();
	self:PlayMove();
end

local ShowLable = function(self)
	self:ShowLable();
	if self.currentLabel ~= nil then
		self.currentLabel:InitData(self);
	end
end
util.hotfix_ex(CS.OPSPanelMissionHolder,'get_CanShow',CanShow)
util.hotfix_ex(CS.OPSPanelMissionHolder,'PlayMove',PlayMove)
util.hotfix_ex(CS.OPSPanelMissionHolder,'ShowLable',ShowLable)


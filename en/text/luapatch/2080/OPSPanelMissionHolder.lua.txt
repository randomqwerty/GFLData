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
	if self.paths.Count == 0 then
		local pos = CS.UnityEngine.Vector2(self.transform.localPosition.x,self.transform.localPosition.y);
		CS.OPSPanelBackGround.Instance:Move(pos, true,0.5, 0, true, CS.OPSPanelBackGround.Instance.holderShowMoveScale);
	end
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


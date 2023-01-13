local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelBackGround)

local OnDrag = function(self)
	if CS.OPSPanelController.Instance.campaionId == -57 then
		local y = CS.UnityEngine.Input.mousePosition.y - self.startPointerPos.y;
		self.targetPosition = self.targetPosition + CS.UnityEngine.Vector2(y*0.5,0);
	end
	self:OnDrag();
end

local Reaset = function(self)
	if self.oldscale == 0 then
		self.oldscale = self.scale;
	end
	self:Reaset();
end

local OpenBackgroundClick = function(self)
	self.CanClick = false;
end
local ResetClockContainer = function(self,play)
	self:ResetClockContainer(play);
	self.CanClick = true;
end
util.hotfix_ex(CS.OPSPanelBackGround,'OnDrag',OnDrag)
util.hotfix_ex(CS.OPSPanelBackGround,'Reaset',Reaset)
util.hotfix_ex(CS.OPSPanelBackGround,'OpenBackgroundClick',OpenBackgroundClick)
util.hotfix_ex(CS.OPSPanelBackGround,'ResetClockContainer',ResetClockContainer)

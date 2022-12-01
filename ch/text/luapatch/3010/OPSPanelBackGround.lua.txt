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
util.hotfix_ex(CS.OPSPanelBackGround,'OnDrag',OnDrag)
util.hotfix_ex(CS.OPSPanelBackGround,'Reaset',Reaset)

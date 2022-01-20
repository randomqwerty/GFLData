local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelBackGround)

local ResetClockContainer = function(self,play)
	if self.container ~= nil and not self.container:isNull() then
		local check = 1.0*self.container:ClearCount() / self.container:AllCount();
		local angle = CS.Mathf.Lerp(0, 180, check);
		CS.OPSPanelController.Instance.order_angle[self.container.id] = angle;
	end
	self:ResetClockContainer(play);
end

util.hotfix_ex(CS.OPSPanelBackGround,'ResetClockContainer',ResetClockContainer)




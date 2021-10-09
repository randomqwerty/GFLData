local util = require 'xlua.util'
local panelController = require("2080/OPSPanelController")
xlua.private_accessible(CS.ImageRotateControl)

local OnDrag = function(self,eventData)
	self:OnDrag(eventData);
	self.angle = CS.Mathf.Clamp(self.angle,angleDragmin, angleDragmax);
end

local CheckAngleTemp = function(self)
	return true;
end
local CheckTransAngle = function(self)
	if self.angleMin < -1 then
		self.angle = CS.Mathf.Clamp(self.angle,angleDragmin, angleDragmax);
	end
	self:CheckTransAngle();
end
util.hotfix_ex(CS.ImageRotateControl,'OnDrag',OnDrag)
util.hotfix_ex(CS.ImageRotateControl,'CheckAngleTemp',CheckAngleTemp)
util.hotfix_ex(CS.ImageRotateControl,'CheckTransAngle',CheckTransAngle)



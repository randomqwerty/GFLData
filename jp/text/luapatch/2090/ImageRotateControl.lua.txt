local util = require 'xlua.util'
xlua.private_accessible(CS.ImageRotateControl)

local CheckTransAngle = function(self)
	self:CheckTransAngle();
	if self.useTransformZ then
		self.transform.localRotation = CS.UnityEngine.Quaternion.Euler(0, 0, self.angle);
	end
end

util.hotfix_ex(CS.ImageRotateControl,'CheckTransAngle',CheckTransAngle)
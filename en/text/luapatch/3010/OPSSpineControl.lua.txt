local util = require 'xlua.util'
xlua.private_accessible(CS.OPSSpineControl)

local CheckSpinePosition = function(self,interData,point)
	self:CheckSpinePosition(interData,point);
	local pos = CS.UnityEngine.Vector2(point.pos.x,point.pos.y);
	self:CheckSpineOrder(pos);
end

util.hotfix_ex(CS.OPSSpineControl,'CheckSpinePosition',CheckSpinePosition)





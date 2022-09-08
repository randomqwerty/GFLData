local util = require 'xlua.util'
xlua.private_accessible(CS.OPSSpineControl)

local BeginInter = function(self,info,point)
	self:BeginInter(info,point);
	local pos = CS.UnityEngine.Vector2(point.pos.x,point.pos.y);
	self:CheckSpineOrder(pos);
end
local EndInter = function(self,point)
	self:EndInter(point);
	local pos = CS.UnityEngine.Vector2(point.pos.x,point.pos.y);
	self:CheckSpineOrder(pos);
end
local Start = function(self)
	self.uiOffset = CS.UnityEngine.Vector3(0,1.8,0);
end
util.hotfix_ex(CS.OPSSpineControl,'BeginInter',BeginInter)
util.hotfix_ex(CS.OPSSpineControl,'Start',Start)
util.hotfix_ex(CS.OPSSpineControl,'EndInter',EndInter)




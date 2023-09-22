local util = require 'xlua.util'
xlua.private_accessible(CS.SpotNightQuad)

local OpenBrightArea = function(self,size,time)
	self.transform:DOKill();
	self:OpenBrightArea(size,time);
end
local CloseBrightArea = function(self,time)
	self.transform:DOKill();
	self:CloseBrightArea(time);
end
util.hotfix_ex(CS.SpotNightQuad,'OpenBrightArea',OpenBrightArea)
util.hotfix_ex(CS.SpotNightQuad,'CloseBrightArea',CloseBrightArea)
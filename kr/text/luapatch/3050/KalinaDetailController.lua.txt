local util = require 'xlua.util'
xlua.private_accessible(CS.KalinaDetailController)

local mInit = function(self,info)
	self:Init(info);
	local canvas = self.transform:GetComponent(typeof(CS.UnityEngine.Canvas));
	if canvas ~=nil then
		canvas.sortingOrder = 15;
	end
end
util.hotfix_ex(CS.KalinaDetailController,'Init',mInit)
local util = require 'xlua.util'
xlua.private_accessible(CS.SpotNightQuad)

local OpenBrightArea = function(self,size,time)
	self:OpenBrightArea(size,time);
	self.transform.localPosition = CS.UnityEngine.Vector3(0,0,50);
	local render = self.transform:GetComponent(typeof(CS.UnityEngine.Renderer));
	render.sortingLayerName = "Background";
	local canvas = self.transform.parent.parent:GetComponent(typeof(CS.UnityEngine.Canvas));
	if canvas ~= nil then
		render.sortingOrder = canvas.sortingOrder;
	end
end

util.hotfix_ex(CS.SpotNightQuad,'OpenBrightArea',OpenBrightArea)





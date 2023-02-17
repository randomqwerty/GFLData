local util = require 'xlua.util'
xlua.private_accessible(CS.NavigationController)
local myStart = function(self)
    self:Start()
	local canvasGR = self.btnTask.gameObject:GetComponent(typeof(CS.UnityEngine.UI.GraphicRaycaster));
	if canvasGR == nil then
		canvasGR = self.btnTask.gameObject:AddComponent(typeof(CS.UnityEngine.UI.GraphicRaycaster));
	end
end
util.hotfix_ex(CS.NavigationController,'Start',myStart)
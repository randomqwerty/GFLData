local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentUIController)

local Awake = function(self)
	self:Awake();
	self.goAbove:SetActive(true);
	local canvas = self.goAbove:AddComponent(typeof(CS.UnityEngine.Canvas));
	self.goAbove:AddComponent(typeof(CS.UnityEngine.UI.GraphicRaycaster));
	canvas.overrideSorting = true;
	canvas.sortingOrder = 19;	
	--canvas.sortingLayerName = "UI";
end

util.hotfix_ex(CS.DeploymentUIController,'Awake',Awake)




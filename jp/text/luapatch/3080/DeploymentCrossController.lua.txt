local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentCrossController)


local Awake = function(self)
	self:Awake();
	local canvas = self.gameObject:AddComponent(typeof(CS.UnityEngine.Canvas));
	canvas.overrideSorting = true;
	canvas.sortingLayerName = "Default";
end


util.hotfix_ex(CS.DeploymentCrossController,'Awake',Awake)


local util = require 'xlua.util'
xlua.private_accessible(CS.FurniturePerformanceController)

local Awake = function(self)
	self:Awake();
	local camera = self.transform:Find("Main Camera"):GetComponent(typeof(CS.UnityEngine.Camera));
	camera.depth = 10;
end

util.hotfix_ex(CS.FurniturePerformanceController,'Awake',Awake)
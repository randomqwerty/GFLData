local util = require 'xlua.util'
xlua.private_accessible(CS.GuideManagerController)

local ContentReload = function(self)
	if self.currentNode == nil then
		CS.UnityEngine.Object.DestroyImmediate(self.gameObject);
		return;
	end
	self:ContentReload();
end
util.hotfix_ex(CS.GuideManagerController,'ContentReload',ContentReload)


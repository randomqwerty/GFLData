local util = require 'xlua.util'
xlua.private_accessible(CS.GuideManagerController)

local mainCamera = function(self)
	if self.target ~= nil then
		local root = CS.UnityEngine.UI.MaskUtilities.FindRootSortOverrideCanvas(self.target);
		if root ~= nil then
			local canvas = root:GetComponent(typeof(CS.UnityEngine.Canvas));
			if canvas.rootCanvas.worldCamera ~= nil then
				return canvas.rootCanvas.worldCamera;
			end
		end
	end
	return self.mainCamera;
end

util.hotfix_ex(CS.GuideManagerController,'get_mainCamera',mainCamera)


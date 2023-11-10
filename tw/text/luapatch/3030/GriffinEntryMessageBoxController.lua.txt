local util = require 'xlua.util'
xlua.private_accessible(CS.GriffinEntryMessageBoxController)

local mInitUIElements = function(self) 
	self:InitUIElements();
	if CS.Utility.loadedLevelName == "Factory" or CS.Utility.loadedLevelName == "StoreRoom" then
		self.canvas.sortingLayerName = "UI";
		self.canvas.sortingOrder = 53;
	end
end

util.hotfix_ex(CS.GriffinEntryMessageBoxController,'InitUIElements',mInitUIElements)


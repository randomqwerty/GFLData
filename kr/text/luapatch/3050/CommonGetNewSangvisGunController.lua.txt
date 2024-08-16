local util = require 'xlua.util'
xlua.private_accessible(CS.CommonGetNewSangvisGunController)

local mStart = function(self)
	self:Start();
	if CS.Utility.loadedLevelName == "StoreRoom" then

		self.canvas.sortingLayerName = "UI";
		self.canvas.sortingOrder = 53;
	end
end

util.hotfix_ex(CS.CommonGetNewSangvisGunController,'Start',mStart)
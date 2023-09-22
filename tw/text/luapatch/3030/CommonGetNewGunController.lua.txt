local util = require 'xlua.util'
xlua.private_accessible(CS.CommonGetNewGunController)

local myStart = function(self)
	if CS.Utility.loadedLevelName == "Factory" or CS.Utility.loadedLevelName == "StoreRoom" then
		self._canvas.sortingLayerName = "UI";
	end
	self:Start()
end
util.hotfix_ex(CS.CommonGetNewGunController,'Start',myStart)
local util = require 'xlua.util'
xlua.private_accessible(CS.CommonGetNewGunController)
xlua.private_accessible(CS.CommonGetNewSangvisGunController)

local myStart = function(self)
	if CS.Utility.loadedLevelName == "Factory" or CS.Utility.loadedLevelName == "StoreRoom" then
		self._canvas.sortingLayerName = "UI";
	end
	self:Start()
end
local sanStart = function(self)
	self:Start()
	if CS.Utility.loadedLevelName == "Factory" then
		self.canvas.sortingLayerName = "UI";
		self.canvas.sortingOrder = 50;
	end
end
util.hotfix_ex(CS.CommonGetNewGunController,'Start',myStart)
util.hotfix_ex(CS.CommonGetNewSangvisGunController,'Start',sanStart)
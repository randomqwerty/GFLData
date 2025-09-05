local util = require 'xlua.util'
xlua.private_accessible(CS.VehicleStatePresetListLabel)

local mCheckSpineLayer = function(self)
	self:CheckSpineLayer();

	if self.vehicleSpine ~=nil and CS.Utility.loadedLevelName=="Dorm" then 
		CS.UIUtils.SetLayer(self.vehicleSpine.gameObject, "UI");
	end 
end
util.hotfix_ex(CS.VehicleStatePresetListLabel,'CheckSpineLayer',mCheckSpineLayer)
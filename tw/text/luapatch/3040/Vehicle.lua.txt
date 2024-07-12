local util = require 'xlua.util'
xlua.private_accessible(CS.Vehicle)
xlua.private_accessible(CS.VehicleComponent)

local mUnequipComponent = function(self,component)
	 
	component.parentVehicleID = 0;
	self:UnequipComponent(component)
end

util.hotfix_ex(CS.Vehicle,'UnequipComponent',mUnequipComponent)


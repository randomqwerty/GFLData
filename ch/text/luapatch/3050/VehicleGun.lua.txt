local util = require 'xlua.util'
xlua.private_accessible(CS.VehicleComponentGun)
xlua.private_accessible(CS.VehicleComponent)

local UpdateVehicleData = function(self)
	if self.component ~= nil then
		self.parent = self.component.parentVehicle
	end
	self:UpdateVehicleData()
end

util.hotfix_ex(CS.VehicleComponentGun,'UpdateVehicleData',UpdateVehicleData)


local util = require 'xlua.util'
xlua.private_accessible(CS.GarageVehiclePlatformController)

local SetShowIndex_New = function(self,index)	
	local newIndex = 0

	self.listShowVehicleInfo:Clear();
    local currentTime = CS.GameData.GetCurrentTimeStamp();
    for i=0,CS.GameData.listVehicleData.Count-1 do
    	local info = CS.GameData.listVehicleData:GetDataByIndex(i)
        if info.launchTime <= currentTime then 
        	self.listShowVehicleInfo:Add(info)

        	if i == index then
    			newIndex = self.listShowVehicleInfo.Count -1
    		end
    	end
	end       

	self:SetShowIndex(newIndex)
end

util.hotfix_ex(CS.GarageVehiclePlatformController,'SetShowIndex',SetShowIndex_New)

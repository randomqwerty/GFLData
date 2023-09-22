local util = require 'xlua.util'
xlua.private_accessible(CS.VehicleStatePresetListCtrl)

local _CheckDataValid = function(self,presetVehicle)
	local removeList = {};
	local removeListIndex = 0;
	
	for k,v in pairs(presetVehicle.dictComponent) do
		if v ~= nil and CS.GameData.listVehicleComponent:GetDataById(v.id) == nil then
			removeList[removeListIndex] = k;
			removeListIndex = removeListIndex + 1;
		end
	end
	for i=1,#removeList do
		presetVehicle.listComponents:Remove(presetVehicle.dictComponent[removeList[i - 1]]);
		presetVehicle.dictComponent[removeList[i - 1]] = nil;
	end
	
	for i=0,presetVehicle.vehicleCrewsArr.Length - 1 do
		local crew = presetVehicle.vehicleCrewsArr[i];
		if(crew ~= nil) then
			if(crew.currentCrewType == CS.VehicleCrew.VehicleCrewType.Gun) then
				if CS.GameData.listGun:GetDataById(crew.crewedGun.id) == nil then
					crew:UpdateCrew(0,-1);
				end
			elseif crew.currentCrewType == CS.VehicleCrew.VehicleCrewType.Sangvis then
				if CS.GameData.listSangvisGun:GetDataById(crew.crewedSangvis.id) == nil then
					crew:UpdateCrew(0,-1);
				end
			end
		end
		
	end
end

util.hotfix_ex(CS.VehicleStatePresetListCtrl,'CheckDataValid',_CheckDataValid)
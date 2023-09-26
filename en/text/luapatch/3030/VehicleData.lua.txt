local util = require 'xlua.util'

local Condition2_CrewBase = function(self,location)
	if self.vehicleCrewsArr.Length <= location then
		return false;
	end
	local crew = self.vehicleCrewsArr[location];
	if crew == nil then
		return false;
	end
	if crew.currentCrewType == CS.VehicleCrew.VehicleCrewType.Gun then
		if crew.crewedGun ~= nil then
			if crew.info.required_level > 0 then
				return crew.crewedGun.level >= crew.info.required_level;
			end
			return true;
		end
	elseif crew.currentCrewType == CS.VehicleCrew.VehicleCrewType.Sangvis then
		if crew.crewedSangvis ~= nil then
			if crew.info.required_level > 0 then
				return crew.crewedSangvis.level >= crew.info.required_level;
			end
			return true;
		end
	elseif crew.currentCrewType == CS.VehicleCrew.VehicleCrewType.Squad then
		if crew.crewedSquad ~= nil then
			if crew.info.required_level > 0 then
				return crew.crewedSquad.level >= crew.info.required_level;
			end
			return true;
		end
	end
	return false;
end

local Condition3_Crew = function(self,location)
	if self.vehicleCrewsArr.Length <= location then
		return false;
	end
	local crew = self.vehicleCrewsArr[location];
	if crew == nil then
		return false;
	end
	if crew.currentCrewType == CS.VehicleCrew.VehicleCrewType.Gun then
		if crew.crewedGun ~= nil then
			if crew.info.required_number > 0 then
				return crew.crewedGun.number >= crew.info.required_number;
			end
			return true;
		end
	elseif crew.currentCrewType == CS.VehicleCrew.VehicleCrewType.Sangvis then
		if crew.crewedSangvis ~= nil then
			if crew.info.required_rank > 0 then
				return crew.crewedSangvis.rank >= crew.info.required_rank;
			end
			return true;
		end
	elseif crew.currentCrewType == CS.VehicleCrew.VehicleCrewType.Squad then
		if crew.crewedSquad ~= nil then
			if crew.info.required_rank > 0 then
				return crew.crewedSquad.rank >= crew.info.required_rank;
			end
			return true;
		end
	end
	return false;
end
util.hotfix_ex(CS.Vehicle,'Condition2_CrewBase',Condition2_CrewBase)
util.hotfix_ex(CS.Vehicle,'Condition3_Crew',Condition3_Crew)
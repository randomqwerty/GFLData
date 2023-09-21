local util = require 'xlua.util'
xlua.private_accessible(CS.VehicleComponent)

local VCCTOR = function(self,...)
	local length = select('#',...);
	if length == 2 then
		local jsonVehicleComponent = select(1,...);
		if jsonVehicleComponent ~= nil and type(jsonVehicleComponent) ~= "number" and jsonVehicleComponent:GetType() == typeof(CS.LitJson.JsonData) then
			if jsonVehicleComponent:Contains("atk_speed") then
				self.vehicleDynamicRate = jsonVehicleComponent:GetValue("atk_speed").Int;
			end
			--组件没有移速
			self.vehicleDynamicSpeed = 0;
			if jsonVehicleComponent:Contains("crit_rate") then
				self.vehicleDynamicCrit = jsonVehicleComponent:GetValue("crit_rate").Int;
			end
			self:UpdateBaseData();
		end
	end
	
end

local _UpdateInfoAfterStrength = function(self,jsonVehicleComponent)
	self:UpdateInfoAfterStrength(jsonVehicleComponent);
	if jsonVehicleComponent:Contains("atk_speed") then
		self.vehicleDynamicRate = jsonVehicleComponent:GetValue("atk_speed").Int;
	end
	--组件没有移速
	self.vehicleDynamicSpeed = 0;
	if jsonVehicleComponent:Contains("crit_rate") then
		self.vehicleDynamicCrit = jsonVehicleComponent:GetValue("crit_rate").Int;
	end
	self:UpdateBaseData();
end

local _InitFriendComponent = function(self,jsonVehicleComponent)
	self:InitFriendComponent(jsonVehicleComponent);
	if jsonVehicleComponent:Contains("atk_speed") then
		self.vehicleDynamicRate = jsonVehicleComponent:GetValue("atk_speed").Int;
	end
	--组件没有移速
	self.vehicleDynamicSpeed = 0;
	if jsonVehicleComponent:Contains("crit_rate") then
		self.vehicleDynamicCrit = jsonVehicleComponent:GetValue("crit_rate").Int;
	end
	self:UpdateBaseData();
end

util.hotfix_ex(CS.VehicleComponent,'.ctor',VCCTOR)
util.hotfix_ex(CS.VehicleComponent,'UpdateInfoAfterStrength',_UpdateInfoAfterStrength)
util.hotfix_ex(CS.VehicleComponent,'InitFriendComponent',_InitFriendComponent)

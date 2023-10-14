local util = require 'xlua.util'
xlua.private_accessible(CS.VehicleStoreCtrl)

local _SpineChangeOneComponent = function(self,slot_id,skin)
	local componentInfo = CS.GameData.listVehicleComponentData:Find( 
		function(co)
			return co.group == skin.GroupID;
		end);
	if componentInfo ~= nil then
		local comTmp = CS.VehicleComponent(slot_id, componentInfo.id);
		comTmp.id = slot_id;
		comTmp.infoid = componentInfo.id;
		self.fakeComponents[slot_id - 1] = comTmp;
	end
	self:SpineChangeOneComponent(slot_id,skin);
	if self.vehicleSpineBuilder ~=nil and self.vehicleSpineBuilder.transform.childCount == 2 then
		if self.vehicleSpineBuilder.transform:GetChild(0) ~=nil then
			CS.Utility.Destroy(self.vehicleSpineBuilder.transform:GetChild(0).gameObject);		
		end
	end
end

local _SpineTakeOffOneSkin = function(self,slot_id)
	local skinOld = 0;
	if self.dicSlotSkin:ContainsKey(slot_id) then
		skinOld = self.dicSlotSkin[slot_id];
	end
	--只考虑初始有皮肤的情况
	if skinOld > 0 then
		local skin = CS.GameData.listVehicleSkinInfo:GetDataById(skinOld);
		local componentInfo = CS.GameData.listVehicleComponentData:Find( 
			function(co)
				return co.group == skin.GroupID;
			end);
		if componentInfo ~= nil then
			self.fakeComponents[slot_id - 1] = CS.VehicleComponent(slot_id, componentInfo.id);
		end
	end
	
	self:SpineTakeOffOneSkin(slot_id);
end
local _ChooseOneSkin = function(self,good,skin)
	local hasGood=false;
	if self.readyBuyGoods.Count >0 then
		hasGood=self.readyBuyGoods:ContainsValue(good);
	end
	
	self:ChooseOneSkin(good,skin);

	if hasGood==true and self.curSelectedSlot~=nil then
		local id = self.curSelectedSlot.slotId;
		if self.readyBuyGoods:ContainsKey(id) then
			self.readyBuyGoods:Remove(id);
		end
	end
end

local _LoadVehicleSpine = function(self)
	if self.vehicleHasChange then
		self.buildComEffectPool:Clear()
	end
	self:LoadVehicleSpine()
end

local _SpineChangeBodySkin = function(self, skin)
	self.buildComEffectPool:Clear()
	self:SpineChangeBodySkin(skin)	
end

local _SpineTakeoffBodySkin = function(self)
	self.buildComEffectPool:Clear()
	self:SpineTakeoffBodySkin()	
end

local _SpineChangeOriginBodySkin = function(self)
	self.buildComEffectPool:Clear()
	self:SpineChangeOriginBodySkin()	
end

util.hotfix_ex(CS.VehicleStoreCtrl,'SpineChangeOneComponent',_SpineChangeOneComponent)
util.hotfix_ex(CS.VehicleStoreCtrl,'SpineTakeOffOneSkin',_SpineTakeOffOneSkin)
util.hotfix_ex(CS.VehicleStoreCtrl,'ChooseOneSkin',_ChooseOneSkin)
util.hotfix_ex(CS.VehicleStoreCtrl,'LoadVehicleSpine',_LoadVehicleSpine)
util.hotfix_ex(CS.VehicleStoreCtrl,'SpineChangeBodySkin',_SpineChangeBodySkin)
util.hotfix_ex(CS.VehicleStoreCtrl,'SpineTakeoffBodySkin',_SpineTakeoffBodySkin)
util.hotfix_ex(CS.VehicleStoreCtrl,'SpineChangeOriginBodySkin',_SpineChangeOriginBodySkin)


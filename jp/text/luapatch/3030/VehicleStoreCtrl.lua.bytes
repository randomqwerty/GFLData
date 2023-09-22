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
util.hotfix_ex(CS.VehicleStoreCtrl,'SpineChangeOneComponent',_SpineChangeOneComponent)
util.hotfix_ex(CS.VehicleStoreCtrl,'SpineTakeOffOneSkin',_SpineTakeOffOneSkin)
util.hotfix_ex(CS.VehicleStoreCtrl,'ChooseOneSkin',_ChooseOneSkin)
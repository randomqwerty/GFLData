local util = require 'xlua.util'
xlua.private_accessible(CS.VehicleSpineBuilder)

local _InitBodySpineSlotData = function(self,clothObj,subClothObjs,vehicleNode)
	local animation = clothObj:GetComponent(typeof(CS.SkeletonAnimation));
	self:InitAnimationSlotData(animation, vehicleNode);
	for i=0,subClothObjs.Count-1 do
		local subAnimation = subClothObjs[i]:GetComponent(typeof(CS.SkeletonAnimation));
		self:InitAnimationSlotData(subAnimation, vehicleNode);
		local _name = tostring(subClothObjs[i].name);
		local nameArray = Split(_name,"_");
		local orderStr = nameArray[#nameArray];
		local order = tonumber(orderStr);
		if self.orderMap:ContainsKey(_name) then
			self.orderMap:Remove(_name);
		end
		self.orderMap:Add(_name,order);
	end
	
	self.orderMap = self:NiXu(self.orderMap);
end


util.hotfix_ex(CS.VehicleSpineBuilder,'InitBodySpineSlotData',_InitBodySpineSlotData)


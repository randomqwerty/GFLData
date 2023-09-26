local util = require 'xlua.util'
xlua.private_accessible(CS.CommonEquipmentListGunInfoController)

local mInitWithGun = function(self,gun,slot)
	self:InitWithGun(gun,slot);
	if gun~=nil and slot > 0 and CS.CommonEquipmentListController.Instance ~=nil then
		CS.CommonEquipmentListController.Instance.btnEquipGroup.gameObject:SetActive(false);
	end
end

util.hotfix_ex(CS.CommonEquipmentListGunInfoController,'InitWithGun',mInitWithGun)


local util = require 'xlua.util'
xlua.private_accessible(CS.EquipGourpEquipListController)

local mInitBtnStatus = function(self,equip)
	self:InitBtnStatus(equip);
	if (self.currentSelectGun ~= nil) and self.has_num>0 then
        if self.currentSelectGun.level < CS.Ratio.arrEquipLevelLimit[self.equipSlot] then
        	self.objCanEquip:SetActive(false);
        end
    end
end

util.hotfix_ex(CS.EquipGourpEquipListController,'InitBtnStatus',mInitBtnStatus)

local util = require 'xlua.util'
xlua.private_accessible(CS.CommonEquipmentListController)

local CreateList  = function(self,...)
	self:CreateList(...);
	if CS.TheaterEchelonSelection.Instance ~= nil and CS.UISimulatorFormation.isExist == true then
		CS.UISimulatorFormation.Instance:SangvisGunPagination(false, false);
	end
	if CS.TheaterEchelonSelection.Instance ~= nil and CS.UISimulatorFormation.isExist == false and self.showEquipWithGun then
		for i=0,self.listFilteredEquip.Count-1 do
			local equip = self.listFilteredEquip[i];
			if equip.currentSortStatus == CS.EquipSortStatus.Normal and equip.gun ~= nil then
				if equip.gun.status == CS.GunStatus.mission or equip.gun.status == CS.GunStatus.operation then
					equip.currentSortStatus = CS.EquipSortStatus.EquipInMissionGun;
				else
					equip.currentSortStatus = CS.EquipSortStatus.EquipInGun;
				end
			end
		end
	end
end

util.hotfix_ex(CS.CommonEquipmentListController,'CreateList',CreateList)
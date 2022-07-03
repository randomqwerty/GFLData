local util = require 'xlua.util'
xlua.private_accessible(CS.ResearchEquipmentStrengthenController)
xlua.private_accessible(CS.CommonEquipmentListController.EquipmentChooseDataEventArgs)
xlua.private_accessible(CS.EquipSorter)
xlua.private_accessible(CS.CommonEquipmentListController)
local _OnOpenEquipmentList = function(self)
   self.mainChosenData.SortMode=false;
   self:OnOpenEquipmentList();
end
local _EquipSorter = function(self, ...)
    local length = select('#', ...);
    if length == 3 then
        if CS.CommonEquipmentListController.inst ~=nil then
            if CS.CommonEquipmentListController.inst.listType == CS.EquipListType.StrengthenFeed then
                self.desc=true;
            end 
        end
    end
end
util.hotfix_ex(CS.ResearchEquipmentStrengthenController,'OnOpenEquipmentList',_OnOpenEquipmentList)
util.hotfix_ex(CS.EquipSorter,'.ctor',_EquipSorter)
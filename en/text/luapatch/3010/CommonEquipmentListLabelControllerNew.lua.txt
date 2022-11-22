local util = require 'xlua.util'
xlua.private_accessible(CS.CommonEquipmentListLabelControllerNew)
local lastLabel;
local myOnPointerClick = function(self)
    self:OnPointerClick()
	if self.parentController ~= nil and self.parentController.listType == CS.EquipListType.EquipPreset then
		if(lastLabel ~= nil) then
			lastLabel.goSelectFrame:SetActive(lastLabel.equip.isSelected);
		end
		lastLabel = self;
	end	
end
util.hotfix_ex(CS.CommonEquipmentListLabelControllerNew,'OnPointerClick',myOnPointerClick)
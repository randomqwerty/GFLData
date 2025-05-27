local util = require 'xlua.util'
xlua.private_accessible(CS.FormationEquipLabelController)

local mInstanceEquipInfoLabel = function(self,equipInfo)
	self:InstanceEquipInfoLabel(equipInfo);
	if self.listlabel~=nil then
		self.listlabel:HideDescription()
	end
end
util.hotfix_ex(CS.FormationEquipLabelController,'InstanceEquipInfoLabel',mInstanceEquipInfoLabel)

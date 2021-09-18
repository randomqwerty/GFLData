local util = require 'xlua.util'
xlua.private_accessible(CS.FactoryDevelopLogListLabelController)

local UpdateInfo = function(self)
	if self.textEquipCategory ~= nil then
		self.textEquipCategory.text = '';
	end
	self:UpdateInfo();
end

util.hotfix_ex(CS.FactoryDevelopLogListLabelController,'UpdateInfo',UpdateInfo)
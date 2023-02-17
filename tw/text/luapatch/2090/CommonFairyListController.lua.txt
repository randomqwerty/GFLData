local util = require 'xlua.util'
xlua.private_accessible(CS.CommonFairyListController)
local CheckNillObject = function(self)
   self:CheckNillObject();
	if self.goNill~= nil and not self.goNill:isNull() then
		self.goNill.transform:SetAsFirstSibling();
	end
end
util.hotfix_ex(CS.CommonFairyListController,'CheckNillObject',CheckNillObject)
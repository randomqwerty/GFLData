local util = require 'xlua.util'
xlua.private_accessible(CS.DormConfirmBox)

local OnInputFieldEndEdit = function(self, a)
	if CS.System.String.IsNullOrEmpty(a) then
		self:OnInputFieldEndEdit("1");
	else
		self:OnInputFieldEndEdit(a);
	end
end

util.hotfix_ex(CS.DormConfirmBox,'OnInputFieldEndEdit',OnInputFieldEndEdit)

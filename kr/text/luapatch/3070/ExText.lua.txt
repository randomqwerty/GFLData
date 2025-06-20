local util = require 'xlua.util'
xlua.private_accessible(CS.ExText)

local InitFunctionSkillTextData = function(self,...)
	self:InitFunctionSkillTextData(...);
	if self.m_Text == "" and self.oringText ~= "" then
		self.m_Text = self.oringText;
	end
end
util.hotfix_ex(CS.ExText,'InitFunctionSkillTextData',InitFunctionSkillTextData)



local util = require 'xlua.util'
xlua.private_accessible(CS.HomeOperationButton)


local Init = function(self)
	self.statementList:Clear();
	self:Init();
	if self.statementList.Count > 0  and self.statementList[0].statement == CS.HomeOperationState.Hide then
		self.gameObject:SetActive(false);
	end
end


util.hotfix_ex(CS.HomeOperationButton,'Init',Init)
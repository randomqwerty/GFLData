local util = require 'xlua.util'
xlua.private_accessible(CS.QuestsController)

local _CreateCareerList = function(self)
	self:CreateCareerList();
	if self.gobjGetAllNode.gameObject.activeSelf then
		self.gobjGetAllNode.gameObject:SetActive(false);
	end
end
util.hotfix_ex(CS.QuestsController,'CreateCareerList',_CreateCareerList)
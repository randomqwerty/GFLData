local util = require 'xlua.util'
xlua.private_accessible(CS.FriendCosmeticIconController)
local _InitUIElements = function(self)
	self:InitUIElements()
	self.btnBuyMore.gameObject:SetActive(true);
end
util.hotfix_ex(CS.FriendCosmeticIconController,'InitUIElements',_InitUIElements)
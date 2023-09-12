local util = require 'xlua.util'
xlua.private_accessible(CS.MallNavigationTab)
xlua.private_accessible(CS.MallController)
xlua.private_accessible(CS.MallGoodClassification)

local _UpdateGroupAppearance = function(self)
	if self.type == CS.MallGoodClassification.FriendShop then
		CS.MallController.Instance:OnClickFriendShop();
		return
	end
	self:UpdateGroupAppearance();
end
util.hotfix_ex(CS.MallNavigationTab,'UpdateGroupAppearance',_UpdateGroupAppearance)
local util = require 'xlua.util'
xlua.private_accessible(CS.MallController)

local OnClickFriendShop = function(self)
	CS.CommonSceneManagerController.instance:PopController();
	self:OnClickFriendShop();
end

util.hotfix_ex(CS.MallController,'OnClickFriendShop',OnClickFriendShop)

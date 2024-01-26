local util = require 'xlua.util'
xlua.private_accessible(CS.MallSkinDisplayItemListController)
local _InitData = function(self)
	if CS.MallController.Instance ~=nil and CS.MallController.Instance.listSkinTheme ~=nil and CS.MallController.Instance.listSkinTheme:Contains(0) then
		CS.MallController.Instance.listSkinTheme:Remove(0);
	end
	self:InitData();
end
util.hotfix_ex(CS.MallSkinDisplayItemListController,'InitData',_InitData)
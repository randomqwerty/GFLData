local util = require 'xlua.util'
xlua.private_accessible(CS.GunStateSkinPageController)
local mInitUIElements = function(self)
	self:InitUIElements()

	local img_bg = self.btnWearBig.transform:Find("Img_WearBG"):GetComponent(typeof(CS.ExImage));
	img_bg.raycastTarget=true;
end
util.hotfix_ex(CS.GunStateSkinPageController,'InitUIElements',mInitUIElements)
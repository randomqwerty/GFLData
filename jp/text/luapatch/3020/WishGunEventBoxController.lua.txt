local util = require 'xlua.util'
xlua.private_accessible(CS.WishGunEventBoxController)

 
local InitUIElements = function(self)
	self:InitUIElements();
	local txtPoint = self.transform:Find("FrameWishGunEvent/EventBundle/DetailsGroup/EventReturnGroup/Tex_Return");
	txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(32341);
end

util.hotfix_ex(CS.WishGunEventBoxController,'InitUIElements',InitUIElements)
local util = require 'xlua.util'
xlua.private_accessible(CS.WishGunEventBoxController)

 

local InitUIElements = function(self)
	self:InitUIElements();
	local trans = self.transform:Find("BlackBackGround"):GetComponent(typeof(CS.UnityEngine.RectTransform));

	trans.offsetMax=CS.UnityEngine.Vector2(trans.offsetMax.x,75)
end
util.hotfix_ex(CS.WishGunEventBoxController,'InitUIElements',InitUIElements)
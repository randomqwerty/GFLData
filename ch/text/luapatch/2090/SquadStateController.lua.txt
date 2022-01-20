local util = require 'xlua.util'
xlua.private_accessible(CS.SquadStateController)

local InitUIElements = function(self)
	self:InitUIElements();
	local bgtrans = self.transform:Find("SquadPic/Image_Squad/Image_BG"):GetComponent(typeof(CS.UnityEngine.RectTransform));
	bgtrans.offsetMin = CS.UnityEngine.Vector2(0, 480);
end

util.hotfix_ex(CS.SquadStateController,'InitUIElements',InitUIElements)


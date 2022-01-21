local util = require 'xlua.util'
xlua.private_accessible(CS.BatchDevelopConfirmBoxController)
local myInit = function(self, types, resourceNum)
    self:Init(types, resourceNum)
	if self.isWish == false then
		self.textWishGunTips.gameObject:SetActive(false);
        self.textWishGunTipsSp.gameObject:SetActive(false);
        self.objWishGunBg:SetActive(false);
        self.objWishGunSpBg:SetActive(false);
	end
end
util.hotfix_ex(CS.BatchDevelopConfirmBoxController,'Init',myInit)
local util = require 'xlua.util'
xlua.private_accessible(CS.FriendChangeAppearanceController)

local RefreshRightCometic = function(self)
	if self.type == CS.CosmeticType.background then
		if self.currentBackgroundId == 0 then
			self.rightImageCardBg.sprite = CS.CommonController.LoadImageSprite("Pics/CardBG/默认背景");
			self.rightcosmeticName.text = "";
			self.rightcosmeticDes.text = "";
			return;
		end
	end		
	self:RefreshRightCometic();

end

util.hotfix_ex(CS.FriendChangeAppearanceController,'RefreshRightCometic',RefreshRightCometic)
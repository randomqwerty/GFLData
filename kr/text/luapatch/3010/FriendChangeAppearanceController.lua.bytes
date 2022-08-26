local util = require 'xlua.util'
xlua.private_accessible(CS.FriendChangeAppearanceController)

local RefreshRightCometic = function(self)
	if self.type == CS.CosmeticType.background then
		if self.currentBackgroundId == 0 then
			self.rightImageCardBg.sprite = CS.CommonController.LoadImageSprite("Pics/CardBG/默认背景");
			self.rightcosmeticName.text = "";
			self.rightcosmeticDes.text = "";
			for i=0,self.comCardBgListController.transform.childCount -1 do
				local child = self.comCardBgListController.transform:GetChild(i);
				if child.childCount>0 then
					local icon = child:GetChild(0):GetComponent(typeof(CS.FriendCosmeticIconController));
					if icon ~= nil then
						icon:CheckPreview();
					end
				end
			end
			return;
		end
	end		
	self:RefreshRightCometic();

end

util.hotfix_ex(CS.FriendChangeAppearanceController,'RefreshRightCometic',RefreshRightCometic)
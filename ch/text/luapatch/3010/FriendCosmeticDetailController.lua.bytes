local util = require 'xlua.util'
xlua.private_accessible(CS.FriendCosmeticDetailController)

local Reset = function(self)
	self.good = nil;
	self.cosmetic = nil;
	self.gameObject:SetActive(true);
	self.buttons:SetActive(true);
	self.coffBg:SetActive(false);
	self.coffBg2:SetActive(false);
	self.windowImg:SetActive(true);	
	self.textQuota.transform.parent.gameObject:SetActive(false);
	self.textGemPrice.transform.parent.gameObject:SetActive(false);
	self.textItemPrice.transform.parent.gameObject:SetActive(false);
	self.textFriendPrice.transform.parent.gameObject:SetActive(false);
	for i=0,self.image.transform.childCount -1 do
		self.image.transform:GetChild(i).gameObject:SetActive(false);
	end
end
--暂时关闭头像框标签
local Open = function(self,data)
	self:Open(data);
	if self.cosmetic ~= nil then	
		if self.cosmetic.type == CS.CosmeticType.headPic then
			CS.CommonController.LoadImageAvatarWithSequenceFrame(self.image, self.cosmetic.id);
		elseif self.cosmetic.type == CS.CosmeticType.headFrame then
			CS.CommonController.LoadImageHeadFrameWithSequenceFrame(self.image, self.cosmetic.id);
		end
	end
end

util.hotfix_ex(CS.FriendCosmeticDetailController,'Reset',Reset)
util.hotfix_ex(CS.FriendCosmeticDetailController,'Open',Open)
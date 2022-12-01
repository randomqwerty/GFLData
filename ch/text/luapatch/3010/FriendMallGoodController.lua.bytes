local util = require 'xlua.util'
xlua.private_accessible(CS.FriendMallGoodController)
local Reset = function(self)
	self.good = nil;
	self.cosmetic = nil;
	self.objSoldOut:SetActive(false);
	self.objNew:SetActive(false);
	self.textType.gameObject:SetActive(false);
	self.textGemPrice.transform.parent.gameObject:SetActive(false);
	self.textItemPrice.transform.parent.gameObject:SetActive(false);
	self.textFriendPrice.transform.parent.gameObject:SetActive(false);
	self.goLive2DTag:SetActive(false);
	for i=0,self.image.transform.childCount -1 do
		self.image.transform:GetChild(i).gameObject:SetActive(false);
	end
end
--local testInit = xlua.get_generic_method(CS.FriendMallGoodController,'Init')
--local testFunUse = testInit(CS.FriendMallGood)
--local testFun1Use = testInit(CS.FriendCosmetic)
--暂时关闭头像框标签
local Init = function(self,data)
	self:Init(data);
	if self.cosmetic ~= nil then	
		if self.cosmetic.type == CS.CosmeticType.headPic then
			CS.CommonController.LoadImageAvatarWithSequenceFrame(self.image, self.cosmetic.id);
		elseif self.cosmetic.type == CS.CosmeticType.headFrame then
			CS.CommonController.LoadImageHeadFrameWithSequenceFrame(self.image, self.cosmetic.id);
		end
	end
end

util.hotfix_ex(CS.FriendMallGoodController,'Reset',Reset)
util.hotfix_ex(CS.FriendMallGoodController,'Init',Init)
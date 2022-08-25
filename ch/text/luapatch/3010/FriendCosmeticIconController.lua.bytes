local util = require 'xlua.util'
xlua.private_accessible(CS.FriendCosmeticIconController)

--暂时关闭头像框购买标签
local Init = function(self,info)
	if info.specialCode == nil then
		self:Init(info);
	else
		self:Init(info);
		if info.type == CS.CosmeticType.headFrame then
			if info.specialCode == "jump" then
				self.goBuyMore:SetActive(false);
				self.goImage.gameObject:SetActive(false);
				self.imageSelect.gameObject:SetActive(false);
			end
		end
	end
end

local CheckPreview = function(self)
	if self.cosmetic ~= nil then
		if self.cosmetic.specialCode == "jump" then
			return;
		end
	end
	self:CheckPreview();
end
util.hotfix_ex(CS.FriendCosmeticIconController,'Init',Init)
util.hotfix_ex(CS.FriendCosmeticIconController,'CheckPreview',CheckPreview)
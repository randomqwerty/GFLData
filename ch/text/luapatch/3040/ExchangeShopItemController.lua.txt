local util = require 'xlua.util'
xlua.private_accessible(CS.ExchangeShopItemController)


local mSetItemDescription = function(self)
	self:SetItemDescription();
	if self.currentMallGood ~= nil and not self.currentMallGood.hasOwn and self.currentMallGood.type == 53 then
		local gift_id = self.currentMallGood.package.listGiftPackage[0].info.id;
		--print("gift_id:"..gift_id);
		local gift_info =CS.GameData.listGiftInfo:GetDataById(gift_id);
		
		if gift_info ~= nil then
			local skin_id = gift_info.skin;
			--print("skin_id:"..skin_id);
			
			local skin = CS.GameData.listSkin:GetDataById(skin_id);
			if skin~=nil then
				self.currentMallGood.hasOwn=true;
			end
			--skin=nil
		end
		--gift_info=nil
	end
end
util.hotfix_ex(CS.ExchangeShopItemController,'SetItemDescription',mSetItemDescription)


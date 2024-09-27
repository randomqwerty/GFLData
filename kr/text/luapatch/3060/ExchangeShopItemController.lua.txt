local util = require 'xlua.util'
xlua.private_accessible(CS.ExchangeShopItemController)

local SetItemDescription = function(self)
	self:SetItemDescription()
	
	if self.currentMallGood.type == 2 and self.currentMallGood.package.listItemPackage.Count > 0 
		and self.currentMallGood.package.listItemPackage[0].info.itemId == 51 then
		self.timeLeft.gameObject:SetActive(false);
	end
end
util.hotfix_ex(CS.ExchangeShopItemController,'SetItemDescription',SetItemDescription)



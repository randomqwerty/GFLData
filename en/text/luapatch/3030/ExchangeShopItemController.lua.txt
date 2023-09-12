local util = require 'xlua.util'
xlua.private_accessible(CS.ExchangeShopItemController)

local _Init = function(self,mallGood)
	self:Init(mallGood);
	if self.gameObject.activeSelf==false then
		self.gameObject:SetActive(true);
	end
end

util.hotfix_ex(CS.ExchangeShopItemController,'Init',_Init)
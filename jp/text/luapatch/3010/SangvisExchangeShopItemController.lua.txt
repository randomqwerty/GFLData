local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisExchangeShopItemController)
xlua.private_accessible(CS.SangvisExchangeShopController)
local myRequestSangvisExchangeMall = function(self,request)
    self:RequestSangvisExchangeMall(request)
	if CS.SangvisExchangeShopController.Instance ~= nil then
		CS.SangvisExchangeShopController.Instance.gameObject:SetActive(false);
	end
end
util.hotfix_ex(CS.SangvisExchangeShopItemController,'RequestSangvisExchangeMall',myRequestSangvisExchangeMall)
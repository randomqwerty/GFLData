local util = require 'xlua.util'
xlua.private_accessible(CS.ServerInfo)

local GenerateOrderId4TxwyPayment = function(self,productId,callback)	
	self:GenerateOrderId4TxwyPayment(productId,callback);
	CS.ConnectionController.print(CS.Data.GetLang(71042));
end


util.hotfix_ex(CS.ServerInfo,'GenerateOrderId4TxwyPayment',GenerateOrderId4TxwyPayment)

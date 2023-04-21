local util = require 'xlua.util'
xlua.private_accessible(CS.HomeController)
xlua.private_accessible(CS.ServerInfo)
xlua.private_accessible(CS.GameData)
xlua.private_accessible(CS.UserRecord)
local mySevenLoginCheck = function(self)
	--print(CS.GameData.userRecord._bpBuyCount)
	if CS.GameData.userRecord ~= nil and CS.GameData.userRecord._bpBuyCount==0 then
		CS.GameData.userRecord._bpBuyCount = CS.GameData.userRecord._bpBuyCount+1;
		CS.GameData.ClearPurchaseGoods();
		CS.ServerInfo.Instance:RequestProductList(
			function ()
				CS.ConnectionController.CloseConsole(); 
			end
		);
	end
    self:SevenLoginCheck()
end

util.hotfix_ex(CS.HomeController,'SevenLoginCheck',mySevenLoginCheck)
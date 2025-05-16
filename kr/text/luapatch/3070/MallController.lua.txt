local util = require 'xlua.util'
xlua.private_accessible(CS.MallController)
xlua.private_accessible(CS.PlayerReturnEventCtrl)
xlua.private_accessible(CS.PlayerReturnFundCtrl)
xlua.private_accessible(CS.PlayerReturnMallCtrl)

local mExitMailResourceLoop = function(hasMail)
	CS.MallController.ExitMailResourceLoop(hasMail);
	if CS.MallController.mallGoodToShip ~=nil then
		if CS.MallController.mallGoodToShip.type == CS.GoodType.payToReturnFund and CS.PlayerReturnEventCtrl.Instance~=nil then
		 	CS.PlayerReturnEventCtrl.Instance.fundCtrl:PayCallBack(hasMail);
		elseif CS.MallController.mallGoodToShip.type == CS.GoodType.payToReturnGiftbag and CS.PlayerReturnEventCtrl.Instance~=nil  then 
			CS.PlayerReturnEventCtrl.Instance.shopCtrl:PayCallBack(hasMail);
		elseif CS.MallController.mallGoodToShip.type == CS.GoodType.payToSkinBlindBox and CS.MallBlindBoxController.Instance~=nil  then 
			CS.MallBlindBoxController.Instance:BuyGoodHandle(CS.MallController.mallGoodToShip);
		end	 	
	end
end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
util.hotfix_ex(CS.MallController,'ExitMailResourceLoop',mExitMailResourceLoop)
end
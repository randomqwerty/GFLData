local util = require 'xlua.util'
xlua.private_accessible(CS.PassOrderController)

local mGoodLiggCallback = function(self)
	self:GoodLiggCallback();
	self.canClickBuybox = true;
end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw then
	util.hotfix_ex(CS.PassOrderController,'GoodLiggCallback',mGoodLiggCallback)
end
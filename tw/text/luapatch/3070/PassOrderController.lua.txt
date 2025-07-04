local util = require 'xlua.util'
xlua.private_accessible(CS.PassOrderController)

local mGoodLiggCallback = function(self)
	self:GoodLiggCallback();
	self.canClickBuybox = true;
end
util.hotfix_ex(CS.PassOrderController,'GoodLiggCallback',mGoodLiggCallback)
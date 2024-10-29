local util = require 'xlua.util'
xlua.private_accessible(CS.MallGoodController)

local ShowPrize = function(self,p)
	CS.PrizeInfoBoxCtrl.ShowTips(p,self.goodName); 
end
util.hotfix_ex(CS.MallGoodController,'ShowPrize',ShowPrize)
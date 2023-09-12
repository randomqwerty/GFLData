local util = require 'xlua.util'
xlua.private_accessible(CS.PassOrderBuyLevelController)
local myDelayCreateCache = function(self,i)
	if(i - 1 >= self.itemDataList.Count) then

	else
		self:DelayCreateCache(i)
	end
end
util.hotfix_ex(CS.PassOrderBuyLevelController,'DelayCreateCache',myDelayCreateCache)
local util = require 'xlua.util'
xlua.private_accessible(CS.PassOrderBuyLevelController)
xlua.private_accessible(CS.PassOrderConfig)
xlua.private_accessible(CS.CommonController)
local myInitData = function(self, itemDataList, currentPassOrder)
    self:InitData(itemDataList, currentPassOrder)
	self:SliderValueChange(CS.PassOrderConfig.Instance.maxCount - 1);
	self:RefreshUI(self.currentSelectLv - self.currentUserLv);
	CS.CommonController.Invoke(function ()
			self:SliderValueChange(self.currentSelectLv - self.currentUserLv);
	end,0.1, CS.PassOrderBuyLevelController.Instance);
end
util.hotfix_ex(CS.PassOrderBuyLevelController,'InitData',myInitData)
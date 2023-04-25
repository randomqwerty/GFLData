local util = require 'xlua.util'
xlua.private_accessible(CS.DailyExploreRewardSliderController)

local _RefreshPrizeLine = function(self)
	self.nextComplete = -1;
	self:RefreshPrizeLine();
	if (self.nextComplete == -1) then
		self:RefreshAllPrizeItemUI();
	end
end


util.hotfix_ex(CS.DailyExploreRewardSliderController,'RefreshPrizeLine',_RefreshPrizeLine)
local util = require 'xlua.util'
xlua.private_accessible(CS.DailyExploreData)
xlua.private_accessible(CS.DailyExploreUIController)

local mRefreshMapStatus = function(self,jsonData,spot_id)
	self:RefreshMapStatus(jsonData,spot_id);
	if (CS.DailyExploreUIController.Instance ~= nil) then
        CS.DailyExploreUIController.Instance.rewardSlider:RefreshUI();
    end
end

util.hotfix_ex(CS.DailyExploreData,'RefreshMapStatus',mRefreshMapStatus)

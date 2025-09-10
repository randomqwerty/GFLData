local util = require 'xlua.util'
xlua.private_accessible(CS.DailyExploreUIController)

local OnClickReturn = function(self)
	self:OnClickReturn();
	if CS.DailyGameAutoPlanController.Status == CS.DailyGameAutoPlanController.PlanStatus.planning then
		CS.DailyGameAutoPlanController.Status = CS.DailyGameAutoPlanController.PlanStatus.normal;
	end
end


util.hotfix_ex(CS.DailyExploreUIController,'OnClickReturn',OnClickReturn)




local util = require 'xlua.util'
xlua.private_accessible(CS.DailyPointPrizeInfo)

local _GetPointRound = function(self)
	if CS.Utility.loadedLevelName == "DailyGame" then
		if self.points >= self.MaxPoint then
			return CS.Mathf.FloorToInt(self.points / self.MaxPoint + 1);
		end
	end
	self:GetPointRound();
	
end
util.hotfix_ex(CS.DailyPointPrizeInfo,'GetPointRound',_GetPointRound)
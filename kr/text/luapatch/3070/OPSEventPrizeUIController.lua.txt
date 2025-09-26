local util = require 'xlua.util'
xlua.private_accessible(CS.OPSEventPrizeUIController)

local ShowDetailTime = function(self)
end
local Init= function(self,data)
	self:Init(data);
	if data ~= nil then
		if not CS.System.String.IsNullOrEmpty(data.prizeLevelInfo.prize_end_time) then
			self.timeDetailLeft.gameObject:SetActive(true);
		else
			self.timeDetailLeft.gameObject:SetActive(false);
		end
	end
end
util.hotfix_ex(CS.OPSEventPrizeUIController,'ShowDetailTime',ShowDetailTime)
util.hotfix_ex(CS.OPSEventPrizeUIController,'Init',Init)
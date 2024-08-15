local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)
local GenerateStoryReviewUrl = function(self)
	local url = self:GenerateStoryReviewUrl()
	if not CS.System.String.IsNullOrEmpty(url) then
		return url..'&channel=game'
	end
	return url
end

util.hotfix_ex(CS.OPSPanelController,'GenerateStoryReviewUrl',GenerateStoryReviewUrl)
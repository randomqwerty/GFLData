local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionCampaignSelectButtonController)
local InitUIElements = function(self)
	self.goNormal:SetActive(true);
	self.goSelected:SetActive(false);
	self.goLock:SetActive(false);
end
util.hotfix_ex(CS.MissionSelectionCampaignSelectButtonController,'InitUIElements',InitUIElements)
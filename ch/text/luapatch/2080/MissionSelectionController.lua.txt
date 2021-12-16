local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionController)

local SetCurrentCampaignAsDefault = function(self)
	self:SetCurrentCampaignAsDefault();
	if CS.MissionSelectionController.currentSelectedCampaignId == -1 then
		CS.MissionSelectionController.currentSelectedCampaignId = 0;
	end
end

util.hotfix_ex(CS.MissionSelectionController,'SetCurrentCampaignAsDefault',SetCurrentCampaignAsDefault)
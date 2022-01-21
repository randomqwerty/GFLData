local util = require 'xlua.util'
xlua.private_accessible(CS.OPSConfig)


local ContainCampaigns = function()
	if CS.OPSConfig.Instance.curMissionEvent ~= nil then
		return CS.OPSConfig.Instance.curMissionEvent.campaignList;
	end
	return CS.System.Collections.Generic.List(CS.System.Int32)();
end


util.hotfix_ex(CS.OPSConfig,'get_ContainCampaigns',ContainCampaigns)
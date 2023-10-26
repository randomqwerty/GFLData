local util = require 'xlua.util'
xlua.private_accessible(CS.LoginController)
--xlua.private_accessible(CS.AIhelpService)

local mReportUpload = function(self)
	self:Start()
	print("mReportUpload")
	local plat = CS.ApplicationConfigData.PlatformChannelId;
	if plat == "ios" or plat == "GWGW" or plat == "GWHF" or plat == "TapTap" then
		local appId_new = "SunbornNetwork_platform_614373e1-b293-4130-a752-7d190897ba8f";

		if CS.ApplicationConfigData.PlatformChannelId == "ios" then
			appId_new = "SunbornNetwork_platform_35917ad1-7e61-4193-ac0a-9535295da641";
		else
			appId_new = "SunbornNetwork_platform_614373e1-b293-4130-a752-7d190897ba8f";
		end 
		local appKey_new = "SUNBORNNETWORK_app_1d1709716ce14af4a1cc10831e839470";
		local domain_new = "SunbornNetwork.aihelpcn.net";
		--print(appId_new);
		--print(appKey_new);
		--print(domain_new);
		CS.AIhelpService.Initialize(appKey_new, domain_new, appId_new);
	end
end
local mInitialize = function(self,appkey,domain,appId)
	local appId_new = "SunbornNetwork_platform_614373e1-b293-4130-a752-7d190897ba8f";

	if CS.ApplicationConfigData.PlatformChannelId == "ios" then
		appId_new = "SunbornNetwork_platform_35917ad1-7e61-4193-ac0a-9535295da641";
	else
		appId_new = "SunbornNetwork_platform_614373e1-b293-4130-a752-7d190897ba8f";
	end 
	local appKey_new = "SUNBORNNETWORK_app_1d1709716ce14af4a1cc10831e839470";
	local domain_new = "SunbornNetwork.aihelpcn.net";
	print(domain_new);
	--CS.AIhelpService._instance = CS.AIhelpService(appKey_new, domain_new, appId_new);
	CS.AIhelpService.Initialize(appKey_new, domain_new, appId_new);
end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then 
    --util.hotfix_ex(CS.LoginController,'Start',mReportUpload)
    if CS.ApplicationConfigData.PlatformChannelId == "ios" or CS.ApplicationConfigData.PlatformChannelId == "TapTap" or CS.ApplicationConfigData.PlatformChannelId == "GWGW" or CS.ApplicationConfigData.PlatformChannelId == "GWHF" then
		--util.hotfix_ex(CS.LoginController,'Start',mReportUpload)
		util.hotfix_ex(CS.AIhelpService,'Initialize',mInitialize)
	end
end

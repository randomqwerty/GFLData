local util = require 'xlua.util'
xlua.private_accessible(CS.LoginController)
xlua.private_accessible(CS.AIhelpService)

local mReportUpload = function(self)
	self:Start()
	local plat = CS.ApplicationConfigData.PlatformChannelId;
	if plat == "ios" or plat == "GWGW" or plat == "GWHF" or plat == "TapTap" then
		-- 线上 最新非强更包 3.0302
		if CS.ConfigData.clientVersion == "3.0301" then

		else
			--线上 老包
			print("线上 老包"..CS.ConfigData.clientVersion)
			if CS.AIHelpSystem.instance ~=nil then
				CS.UnityEngine.Object.DestroyImmediate(CS.AIHelpSystem.instance.gameObject);
				CS.AIHelpSystem.instance=nil; 
				print("delete old object")
			end 
			local obj = CS.UnityEngine.Object.Instantiate(CS.UnityEngine.Resources.Load("UGUIPrefabs/System/AIHelpSystem"));
			obj.name = "AiHelpSystem2"
		end	
	end
end
local mInitialize = function(self,appkey,domain,appId)
	local domain_new = "SunbornNetwork.aihelpcn.net";
	print(domain_new);
	CS.AIhelpService._instance = CS.AIhelpService(appkey, domain_new, appId);
end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then 
    --util.hotfix_ex(CS.LoginController,'Start',mReportUpload)//CS.ApplicationConfigData.PlatformChannelId == "ios" or 
    if CS.ApplicationConfigData.PlatformChannelId == "TapTap" or CS.ApplicationConfigData.PlatformChannelId == "GWGW" or CS.ApplicationConfigData.PlatformChannelId == "GWHF" then
		util.hotfix_ex(CS.AIhelpService,'Initialize',mInitialize)
	end
end

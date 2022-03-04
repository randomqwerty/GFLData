local util = require 'xlua.util'
xlua.private_accessible(CS.LoginController)
xlua.private_accessible(CS.HotUpdateController)
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
	if(CS.ApplicationConfigData.PlatformChannelId == "ios") then
		xlua.private_accessible(CS.SunBornUserCenter)
	end
end
xlua.private_accessible(CS.ApplicationConfigData)
xlua.private_accessible(CS.SDKAdapter)
xlua.private_accessible(CS.ConnectionController)
local myStartInit = function(self)
    self:StartInit();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		if(CS.ApplicationConfigData.PlatformChannelId == "ios") then
			if CS.System.String.IsNullOrEmpty(CS.ConnectionController.currentServer.heart_addr) then
				CS.SunBornUserCenter.Instance:SetSunbornSDK("ReportURL", "https://fcm.sunborngame.com/index");
			end
			
		end	
	end
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Japan then
		CS.ResCenter._SaveNormal(true);
	end
end
local myEnterGame = function()
	CS.LoginController.EnterGame();
--	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		if(CS.ApplicationConfigData.PlatformChannelId == "ios") then
			CS.SDKAdapter.SDKTrackUserLogin();
		end	
--	end
end

util.hotfix_ex(CS.LoginController,'StartInit',myStartInit)
util.hotfix_ex(CS.LoginController,'EnterGame',myEnterGame)

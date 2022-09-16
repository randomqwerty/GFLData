local util = require 'xlua.util'
xlua.private_accessible(CS.LoginController)
xlua.private_accessible(CS.HotUpdateController)
xlua.private_accessible(CS.ApplicationConfigData) 
 
xlua.private_accessible(CS.ServerInfo) 
local myEnterGame = function()
	CS.LoginController.EnterGame();
	CS.ServerInfo.Instance.SERVER_ADDR ="http://gfcn-transit.tx.sunborngame.com/index.php"; 
end
local _GetChannelId = function(self)
	if CS.GameData.userInfo ~= nil and CS.ConnectionController.currentServer~=nil then
		if CS.ApplicationConfigData.PlatformChannelId == "ios" and CS.ConnectionController.currentServer.worldId=="1000" then
			return "cn_mica";
		elseif CS.ApplicationConfigData.PlatformChannelId == "GWGW" and CS.ConnectionController.currentServer.worldId=="3000" then
			return "cn_appstore";
		elseif CS.ApplicationConfigData.PlatformChannelId == "TapTap" and CS.ConnectionController.currentServer.worldId=="3000" then
			return "cn_appstore";
		else
			--print("111"..CS.ApplicationConfigData.GetChannelId());
			return CS.ApplicationConfigData.GetChannelId();
		end
	else 
		--print("000"..CS.ApplicationConfigData.GetChannelId());
		return CS.ApplicationConfigData.GetChannelId();
	end

end

if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
	if(CS.ApplicationConfigData.PlatformChannelId == "TX") then
		util.hotfix_ex(CS.LoginController,'EnterGame',myEnterGame) 
	end
end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
	if CS.ApplicationConfigData.PlatformChannelId == "ios" or CS.ApplicationConfigData.PlatformChannelId == "TapTap" or CS.ApplicationConfigData.PlatformChannelId == "GWGW" then
		util.hotfix_ex(CS.ApplicationConfigData,'GetChannelId',_GetChannelId)
	end
end
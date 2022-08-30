local util = require 'xlua.util'
xlua.private_accessible(CS.LoginController)
xlua.private_accessible(CS.HotUpdateController)
xlua.private_accessible(CS.ApplicationConfigData) 
 
xlua.private_accessible(CS.ServerInfo) 
local myEnterGame = function()
	CS.LoginController.EnterGame();
	CS.ServerInfo.Instance.SERVER_ADDR ="http://gfcn-transit.tx.sunborngame.com/index.php";
end

if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
	if(CS.ApplicationConfigData.PlatformChannelId == "TX") then
		util.hotfix_ex(CS.LoginController,'EnterGame',myEnterGame)
	end
end 

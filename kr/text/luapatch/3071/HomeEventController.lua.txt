local util = require 'xlua.util'
xlua.private_accessible(CS.HomeEventController)

local mOpenEvent = function(jumpType)
	CS.HomeEventController.canShowEvent=true;
	if CS.CommonController.sceneJumpName=="Home"then 
		CS.HomeEventController.OpenEvent(jumpType)
	elseif CS.CommonController.sceneJumpName=="" and CS.Utility.loadedLevelName=="Home" then
		CS.HomeEventController.OpenEvent(jumpType)
	end 
end
local mLoadSytemNoticeWebview = function(self)
	-- ePlatform_Normal ePlatform_US
	if CS.ApplicationConfigData.PlatformChannelId == "pc" then
		if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Japan then
			CS.MicaTools.OpenURL("https://gf-jp.sunborngame.com/")
		elseif CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_US then
			CS.MicaTools.OpenURL("https://gf.sunborngame.com/")
		else
			self:LoadSytemNoticeWebview();	 
		end
	else
		self:LoadSytemNoticeWebview();	 
	end
end
util.hotfix_ex(CS.HomeEventController,'OpenEvent',mOpenEvent)
util.hotfix_ex(CS.HomeEventController,'LoadSytemNoticeWebview',mLoadSytemNoticeWebview)
local util = require 'xlua.util'
xlua.private_accessible(CS.HomeController)
xlua.private_accessible(CS.ResCenter)
xlua.private_accessible(CS.PassOrderController)
--修正home界面下载对话框显示
local SevenLoginHandler = function(self)
	self:SevenLoginHandler(); 
	if CS.ResCenter.instance.currentDownloadState ~= CS.ResCenter.DownloadAddState.DownloadAddInHome and 
		CS.ResCenter.instance.currentDownloadVoiceState ~= CS.ResCenter.DownloadVoiceState.DownloadInHome then
		return;
	end
	if CS.ResCenter.instance.resDownload ~= nil and not CS.ResCenter.instance.resDownload:isNull() then
		CS.ResCenter.instance.resDownload:Hide();
	end
end

local myOnApplicationFocus = function(self, isFocus)
	if isFocus == true then
		if((CS.PassOrderController.Instance ~= nil and CS.PassOrderController.Instance.gameObject.activeInHierarchy)) then
			
		else
			self:OnApplicationFocus(isFocus); 
		end
	end
end
local myCheckPassOrderScaleUI = function(self, isScale)
	if(isScale == false) then
		if (CS.PassOrderConfig.Instance.passEnter == true and CS.PassOrderUserData.Instance:HasActivePassOrder() ~= nil) then
			self.btnPassObj:SetActive(true);
		end
		else
	self:CheckPassOrderScaleUI(isScale)
	end
end
util.hotfix_ex(CS.HomeController,'SevenLoginHandler',SevenLoginHandler)
--util.hotfix_ex(CS.HomeController,'OnApplicationFocus',myOnApplicationFocus)
util.hotfix_ex(CS.HomeController,'CheckPassOrderScaleUI',myCheckPassOrderScaleUI)





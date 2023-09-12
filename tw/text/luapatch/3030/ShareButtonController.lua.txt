local util = require 'xlua.util'
xlua.private_accessible(CS.ShareButtonController)
local _InitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		print(1111);
		if CS.ApplicationConfigData.PlatformChannelId == "MI" then
			self.gameObject:SetActive(false);
		end
	end
end

if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
	if CS.ApplicationConfigData.PlatformChannelId == "MI" then
		util.hotfix_ex(CS.ShareButtonController,'InitUIElements',_InitUIElements)		
	end 
end

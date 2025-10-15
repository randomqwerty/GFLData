local util = require 'xlua.util'
xlua.private_accessible(CS.SunBornUserCenter)

local mTrackUserThirdPay = function(self,price,currency,productId,name)
	
	if CS.ApplicationConfigData.PlatformChannelId == "pc" then
		if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_US then
			currency='USD';
		elseif CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Japan then
			currency='JPY';
		end
	end
	self:TrackUserThirdPay(price,currency,productId,name);
end

if CS.ApplicationConfigData.PlatformChannelId == "pc" then
	util.hotfix_ex(CS.SunBornUserCenter,'TrackUserThirdPay',mTrackUserThirdPay)
end
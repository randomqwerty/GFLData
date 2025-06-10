local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSkipController)


local ShowComfiromBox = function(self,stage,price,title)
	if CS.GameData.userInfo.gem < price then
		CS.CommonController.LightMessageTips(CS.Data.GetLang(1279));
		return;
	end
	local showtext = CS.System.String.Format(CS.Data.GetLang(40514), tostring(price));
	CS.CommonController.ConfirmBox(showtext ,function()
			self:OnClickUncloak(stage);
		end)
end

util.hotfix_ex(CS.MissionSkipController,'ShowComfiromBox',ShowComfiromBox)

local util = require 'xlua.util'
xlua.private_accessible(CS.MallGoodController)
xlua.private_accessible(CS.HotUpdateController)
xlua.private_accessible(CS.CommonController)
xlua.private_accessible(CS.ApplicationConfigData)
local myOnClick = function(self)
	if self.good ~= nil and (self.good.rmbId == "60101" or self.good.rmbId == "60102" or self.good.rmbId == "60103"
			or self.good.rmbId == "60104" or self.good.rmbId == "60105" or self.good.rmbId == "60106" 
			or self.good.rmbId == "60107" or self.good.rmbId == "60112" or self.good.rmbId == "60151") then
		CS.CommonController.LightMessageTips("この商品は現在購入できません。");
	else
		self:OnClick();  
	end
end 
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Japan and CS.ApplicationConfigData.PlatformChannelId == "ios" then
	util.hotfix_ex(CS.MallGoodController,'OnClick',myOnClick)
end
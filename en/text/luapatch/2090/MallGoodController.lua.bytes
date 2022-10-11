local util = require 'xlua.util'
xlua.private_accessible(CS.MallGoodController)
xlua.private_accessible(CS.HotUpdateController)
xlua.private_accessible(CS.CommonController)
xlua.private_accessible(CS.ApplicationConfigData)
local myOnClick = function(self)
	if self.good ~= nil and (self.good.rmbId == "60112") then
		CS.CommonController.LightMessageTips("この商品は現在購入できません。");
	else
		self:OnClick();  
	end
end 
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Japan and CS.ApplicationConfigData.PlatformChannelId == "ios" then
	util.hotfix_ex(CS.MallGoodController,'OnClick',myOnClick)
end
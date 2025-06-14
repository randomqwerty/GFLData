local util = require 'xlua.util'
xlua.private_accessible(CS.HomeUserInfoNewController)
local mClose = function(self)
	if self.friendNodeHolder.gameObject.activeSelf == true then
		self:CloseUserCard()
	end
	self:Close()
end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
util.hotfix_ex(CS.HomeUserInfoNewController,'Close',mClose)
end
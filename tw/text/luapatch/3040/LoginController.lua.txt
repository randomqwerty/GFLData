local util = require 'xlua.util'
xlua.private_accessible(CS.LoginController)
local myStartInit = function(self)
    self:StartInit();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_US then
		self.btnUserPrivacy:SetActive(true);
	end
end

util.hotfix_ex(CS.LoginController,'StartInit',myStartInit)

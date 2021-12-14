local util = require 'xlua.util'
xlua.private_accessible(CS.HomeController)

local InitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		CS.ConfigData.showHurt=true;
		CS.ConfigData.showHurtNORMAL=true;
		print("强制开启大破")
	end
end

util.hotfix_ex(CS.HomeController,'InitUIElements',InitUIElements)




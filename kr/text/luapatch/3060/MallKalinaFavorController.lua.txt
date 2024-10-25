local util = require 'xlua.util'
xlua.private_accessible(CS.MallKalinaFavorController)

local Init = function(self)
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		self.hasInit = false;
	end
	self:Init();
end
util.hotfix_ex(CS.MallKalinaFavorController,'Init',Init)
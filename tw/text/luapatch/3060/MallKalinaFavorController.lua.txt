local util = require 'xlua.util'
xlua.private_accessible(CS.MallKalinaFavorController)
xlua.private_accessible(CS.MallController)

local LoadNpc = function(self)
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		if self.kalinaFavorController ~= nil then
			self.kalinaFavorController:Init();
		end
		return;
	end
	self:LoadNpc();
end
--util.hotfix_ex(CS.MallKalinaFavorController,'Init',Init)
util.hotfix_ex(CS.MallController,'LoadNpc',LoadNpc)
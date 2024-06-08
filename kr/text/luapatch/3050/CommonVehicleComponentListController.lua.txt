local util = require 'xlua.util'
xlua.private_accessible(CS.CommonVehicleComponentListController)

local Start = function(self)
	self:Start();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local text = self.transform:Find("Left/list/Items/AffixTopping/ToppingItem/Text_Affix"):GetComponent(typeof(CS.ExText));
		text.text = CS.Data.GetLang(290188);
	end
end
util.hotfix_ex(CS.CommonVehicleComponentListController,'Start',Start)


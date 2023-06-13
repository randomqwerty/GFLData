local util = require 'xlua.util'
xlua.private_accessible(CS.FormationShowEquipInfoController)
local Awake = function(self)
	self:Awake();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local tex = self.transform:Find("Detail/AttriLayout/txRateMax/txName"):GetComponent(typeof(CS.ExText));
		tex.text = CS.Data.GetLang(10204);
	end
end

util.hotfix_ex(CS.FormationShowEquipInfoController,'Awake',Awake)
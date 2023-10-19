local util = require 'xlua.util'
xlua.private_accessible(CS.AdjustAdjutantScaleController)

local Awake = function(self)
	self:Awake();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtPoint = self.transform:Find("Assistants/Title/Btn_Title/Tex_Title");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(100326);
	end
end

util.hotfix_ex(CS.AdjustAdjutantScaleController,'Awake',Awake)
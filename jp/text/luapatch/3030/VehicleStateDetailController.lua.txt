local util = require 'xlua.util'
xlua.private_accessible(CS.VehicleStateDetailController)

local _InitUIElements = function(self)
	self:InitUIElements();
	self.btneffectiveness.gameObject:SetActive(false);
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtPoint = self.transform:Find("Main/Detail/ComponentInfo/ComponentRollSkill/ComponentRollSkillTitle/Text_ComponentRollSkil");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(290115);
		txtPoint = self.transform:Find("Main/Detail/CurrentComponentInfo/ComponentRollSkill/ComponentRollSkillTitle/Text_ComponentRollSkil");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(290115);
	end
end


util.hotfix_ex(CS.VehicleStateDetailController,'InitUIElements',_InitUIElements)
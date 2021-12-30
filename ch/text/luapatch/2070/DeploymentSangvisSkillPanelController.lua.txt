local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentSangvisSkillPanelController)

local _InitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		local text1 =self.supportTransfom:Find("SupportSkill/Tex_Name"):GetComponent(typeof(CS.ExText));
		local text2 =self.supportTransfom:Find("SupportSkill/Level/UI_Text"):GetComponent(typeof(CS.ExText));
		text1.resizeTextForBestFit=true;
		text2.resizeTextForBestFit=true;	
	end
end

util.hotfix_ex(CS.DeploymentSangvisSkillPanelController,'InitUIElements',_InitUIElements)
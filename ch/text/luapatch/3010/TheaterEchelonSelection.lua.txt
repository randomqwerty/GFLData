local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterEchelonSelection)

local InitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		local txt1 = self.transform:Find("Right/TheaterEchelonSelectionEnemyInfo/Top_Filter/Btn_Normal/UI_Text");
		txt1:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(210105);
		local txt2 = self.transform:Find("Right/TheaterEchelonSelectionEnemyInfo/Top_Filter/Btn_ACE/Title/UI_Text");
		txt2:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(210104);
		local txt3 = self.transform:Find("Left/Holder/TheaterFormationTile/Panel/ChangeCaptain/On/Tex_Information");
		txt3:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(210300);
	end
end


util.hotfix_ex(CS.TheaterEchelonSelection,'InitUIElements',InitUIElements)
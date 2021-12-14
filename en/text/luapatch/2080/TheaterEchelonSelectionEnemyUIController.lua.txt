local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterEchelonSelectionEnemyUIController)

local InitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		local UI_Text = self.transform:Find("AceNode/UI_Text");
		if UI_Text ~= nil then
			UI_Text:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(210101);
		end
	end
end

util.hotfix_ex(CS.TheaterEchelonSelectionEnemyUIController,'InitUIElements',InitUIElements)
local util = require 'xlua.util'
xlua.private_accessible(CS.FairyStateBuffController)

local _InitUIElements = function(self)
	self:InitUIElements();
	local txt1 = self.transform:Find("Img_Title/UI_Text"):GetComponent(typeof(CS.ExText));
	txt1.text = CS.Data.GetLang(130047);
end

util.hotfix_ex(CS.FairyStateBuffController,'InitUIElements',_InitUIElements)
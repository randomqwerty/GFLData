local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterInvestigationUIController)

local InitUIElements = function(self)
	self:InitUIElements();
	local txt = self.transform:Find("Frame/Right/SPYResult/Tex_Result"):GetComponent(typeof(CS.ExText));
	txt.text = CS.Data.GetLang(210167);
end
util.hotfix_ex(CS.TheaterInvestigationUIController,'InitUIElements',InitUIElements)

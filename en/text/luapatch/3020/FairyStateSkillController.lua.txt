local util = require 'xlua.util'
xlua.private_accessible(CS.FairyStateSkillController)

local _InitUIElements = function(self)
	self:InitUIElements();
	if self.currentLoadLevel == CS.FairyLoadLevel.IllustratedBook then
		self.btnSwitchLevelMax.gameObject:SetActive(true);
		self.objLevelMax:SetActive(true);
	end
end

util.hotfix_ex(CS.FairyStateSkillController,'InitUIElements',_InitUIElements)
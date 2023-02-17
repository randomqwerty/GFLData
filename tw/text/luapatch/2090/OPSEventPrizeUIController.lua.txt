local util = require 'xlua.util'
xlua.private_accessible(CS.OPSEventPrizeUIController)

local InitUIElements = function(self)
	self:InitUIElements();
	self.imgBackground.transform:SetSiblingIndex(2);
end

util.hotfix_ex(CS.OPSEventPrizeUIController,'InitUIElements',InitUIElements)

local util = require 'xlua.util'
xlua.private_accessible(CS.VehicleStateDetailController)

local _InitUIElements = function(self)
	self:InitUIElements();
	self.btneffectiveness.gameObject:SetActive(false);
end


util.hotfix_ex(CS.VehicleStateDetailController,'InitUIElements',_InitUIElements)
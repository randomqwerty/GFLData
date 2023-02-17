local util = require 'xlua.util'
xlua.private_accessible(CS.OPSEventPrizeUIController)
xlua.private_accessible(CS.OPSEventPrizeItemController)

local _InitUIElements = function(self)
	local temp=0;
	if self.existPrizeToGet==true then
		temp=1;	
	end
	self:InitUIElements();
	if temp ==1 then
		self.existPrizeToGet=true;
	end	
end 
local _InitUIElements_Item = function(self)
	 
end 
util.hotfix_ex(CS.OPSEventPrizeUIController,'InitUIElements',_InitUIElements)
util.hotfix_ex(CS.OPSEventPrizeItemController,'InitUIElements',_InitUIElements_Item)
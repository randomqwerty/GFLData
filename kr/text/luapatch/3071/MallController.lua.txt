local util = require 'xlua.util'
xlua.private_accessible(CS.MallController)

local InitUIElements = function(self)	
	self:InitUIElements();
	local canvas = self.transform:Find("Background").gameObject:AddComponent(typeof(CS.UnityEngine.Canvas));
	canvas.overrideSorting = true;
	canvas.sortingOrder = -1; 
end


util.hotfix_ex(CS.MallController,'InitUIElements',InitUIElements)

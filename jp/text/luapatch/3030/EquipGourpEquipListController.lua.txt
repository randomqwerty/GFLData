local util = require 'xlua.util'
xlua.private_accessible(CS.EquipGourpEquipListController)

local mInitUIElements = function(self)
	self.objNotHave:AddComponent(typeof(CS.ExButton));
end

util.hotfix_ex(CS.EquipGourpEquipListController,'InitUIElements',mInitUIElements)


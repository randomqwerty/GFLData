local util = require 'xlua.util'
xlua.private_accessible(CS.VehicleFormationData)

local mCheckSkinHaveChange = function(self)
	if self.skinDict:ContainsKey(-1) == false then
		 self.skinDict:Add(-1,0);
	end
	return self:CheckSkinHaveChange(); 
end

util.hotfix_ex(CS.VehicleFormationData,'CheckSkinHaveChange',mCheckSkinHaveChange)
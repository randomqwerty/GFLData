local util = require 'xlua.util'
xlua.private_accessible(CS.LoginController)

local StartInit = function(self)
	self:StartInit();
	CS.ResManager.prefab_usevision:Clear();
end

util.hotfix_ex(CS.LoginController,'StartInit',StartInit)



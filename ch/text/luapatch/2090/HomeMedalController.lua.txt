local util = require 'xlua.util'
xlua.private_accessible(CS.HomeMedalController)
local InitData_New = function(self, ...)
	self.OpenEffect = false
    self:InitData(...)
end
util.hotfix_ex(CS.HomeMedalController,'InitData',InitData_New)
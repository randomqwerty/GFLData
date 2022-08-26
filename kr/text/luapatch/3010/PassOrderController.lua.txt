local util = require 'xlua.util'
xlua.private_accessible(CS.PassOrderController)
local myScrollCallBack = function(self,index)
    self.specialItem.isSpecialView = false;
    self:ScrollCallBack(index)
end
util.hotfix_ex(CS.PassOrderController,'ScrollCallBack',myScrollCallBack)
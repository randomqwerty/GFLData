local util = require 'xlua.util'
xlua.private_accessible(CS.BingoTaskController)
xlua.private_accessible(CS.CommonSceneManagerController)
local myJump = function(self)
    self:Jump()
	CS.CommonSceneManagerController.instance:Clear();
end
util.hotfix_ex(CS.BingoTaskController,'Jump',myJump)
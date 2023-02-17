local util = require 'xlua.util'
xlua.private_accessible(CS.SpotAction)

local LoadBattleBuff = function(self)
	self:LoadBattleBuff();
	self.listFriendBuffAction = CS.System.Collections.Generic.List(CS.BuffAction)(self.allListFriendBuffAction);
	self.listEnemyBuffAction = CS.System.Collections.Generic.List(CS.BuffAction)(self.allListEnemyBuffAction);
end

util.hotfix_ex(CS.SpotAction,'LoadBattleBuff',LoadBattleBuff)



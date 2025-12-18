local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleManager)
xlua.private_accessible(CS.GF.Battle.BattleController)

local CollectBeforeBattleData = function(self)
	print("BattleManager not anti")
	return nil
end
local NeedUploadAntiData = function(self,type)
	type = -1;

	print("BattleController not anti")
	return false
end
util.hotfix_ex(CS.GF.Battle.BattleManager,'CollectBeforeBattleData',CollectBeforeBattleData)
util.hotfix_ex(CS.GF.Battle.BattleController,'NeedUploadAntiData',NeedUploadAntiData)
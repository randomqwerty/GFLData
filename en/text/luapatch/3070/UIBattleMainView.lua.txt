local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Tarkov.UIBattleMainView)

local OnApplicationUnfocus = function(self)
	
end

util.hotfix_ex(CS.GF.Tarkov.UIBattleMainView,'OnApplicationUnfocus',OnApplicationUnfocus)



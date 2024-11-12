local util = require 'xlua.util'
xlua.private_accessible(CS.TarkovBattleWrapper)
xlua.private_accessible(CS.GF.Battle.BattleController)


local OnBattleEnd = function()
	CS.TarkovBattleWrapper.OnBattleEnd()
	CS.TarkovBattleWrapper.Dispose()

end

util.hotfix_ex(CS.TarkovBattleWrapper,'OnBattleEnd',OnBattleEnd)



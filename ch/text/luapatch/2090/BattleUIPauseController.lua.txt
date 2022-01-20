local util = require 'xlua.util'
xlua.private_accessible(CS.BattleUIPauseController)



local OnClickRestartBattle = function(self)
	if CS.BattleFrameManager.IsStopTime() then
		return
	end
	self:OnClickRestartBattle()
end
util.hotfix_ex(CS.BattleUIPauseController,'OnClickRestartBattle',OnClickRestartBattle)

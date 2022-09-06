local util = require 'xlua.util'
xlua.private_accessible(CS.BattleInteractionController)
local TriggerDragingBulletTime = function(self)
	if CS.GF.Battle.BattleController.Instance.isBattleFinished then
		return
	end
	self:TriggerDragingBulletTime()
end
local TriggerSelectingBulletTime = function(self)
	if CS.GF.Battle.BattleController.Instance.isBattleFinished then
		return
	end
	self:TriggerSelectingBulletTime()
end
util.hotfix_ex(CS.BattleInteractionController,'TriggerSelectingBulletTime',TriggerSelectingBulletTime)
util.hotfix_ex(CS.BattleInteractionController,'TriggerDragingBulletTime',TriggerDragingBulletTime)
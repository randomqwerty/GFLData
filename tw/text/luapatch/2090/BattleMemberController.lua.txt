local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleController)
xlua.private_accessible(CS.BattleMemberController)
local Die = function(self)
	self:Die()
	local battlespot = CS.GF.Battle.BattleController.Instance.currentSpotAction
	if battlespot ~= nil and battlespot.fightTypeInfo ~= nil and battlespot.fightTypeInfo:GetID() == 2 then
		self.animator:Play("Disappear")
	end
end

util.hotfix_ex(CS.BattleMemberController,'Die',Die)

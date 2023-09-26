local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleFieldTeamHolderNew)
xlua.private_accessible(CS.GF.Battle.BattleCharacterManager)
xlua.private_accessible(CS.GF.Battle.BattleMemberManager)
local FP = CS.TrueSync.FP
local UpdateTargetsInRange = function(self,pos,skillCfg,createCfg,rotate)
	--print(self.listCharacter.Count)
	if self.listCharacter.Count > 10 then
		self.UNIT_RADIUS = FP.FromFloat(1.82)
	else
		self.UNIT_RADIUS = FP.FromFloat(0.4)
	end
	self:UpdateTargetsInRange(pos,skillCfg,createCfg,rotate)
end

util.hotfix_ex(CS.GF.Battle.BattleFieldTeamHolderNew,'UpdateTargetsInRange',UpdateTargetsInRange)
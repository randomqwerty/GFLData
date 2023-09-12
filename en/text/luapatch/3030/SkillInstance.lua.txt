local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.CSkillInstance)
xlua.private_accessible(CS.GF.Battle.BattleFieldTeamHolderNew)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)

local _GetRandomOffset = function(self,pEvent)
	local offset = CS.GF.Battle.BattleDynamicData.friendlyTeamHolder.friendlyStartingPos
	if pEvent.EffectCfg.target == 3 then
		return self:_GetRandomOffset(pEvent) - offset
	end
	if pEvent.EffectCfg.target == 4 then
		return self:_GetRandomOffset(pEvent) - CS.TrueSync.TSVector(0,offset.y,offset.z)
	end
	if pEvent.EffectCfg.target == 5 then
		return self:_GetRandomOffset(pEvent) - CS.TrueSync.TSVector(offset.x,0,offset.z)
	end
	return self:_GetRandomOffset(pEvent)
end

util.hotfix_ex(CS.GF.Battle.CSkillInstance,'_GetRandomOffset',_GetRandomOffset)
xlua.private_accessible(CS.BattleFieldTeamHolder)
local util = require 'xlua.util'
local CastAoeBuffDebuff = function(self,caster, debuffSourcePosition, skillCfg, buffCfgID, createCfg, count)
	if count < 0 then
		self:UpdateTargetsInRAnge(debuffSourcePosition, skillCfg, createCfg)
		for i=0,self.mResInRange.Count-1 do
			local buffcfg = CS.GameData.listBTBuffCfg:GetDataById(buffCfgID)
			if buffcfg ~= nil and buffcfg:IsAvailableOnTarget(self.mResInRange[i]) then
				self.mResInRange[i].conditionListSelf:RemoveNum(buffCfgID,-count)
			end
		end
		self.mResInRange:Clear()
	else
		self:CastAoeBuffDebuff(caster, debuffSourcePosition, skillCfg, buffCfgID, createCfg, count)
	end
	
end

util.hotfix_ex(CS.BattleFieldTeamHolder,'CastAoeBuffDebuff',CastAoeBuffDebuff)

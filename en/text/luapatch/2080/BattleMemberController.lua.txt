local util = require 'xlua.util'
xlua.private_accessible(CS.BattleMemberController)
xlua.private_accessible(CS.GF.Battle.BattleCharacterController)
local InitNormalBattle = function(self)
	local PlaySkill = function(self,skill,target)
		if skill:GetType() == typeof(CS.BattleSkillCfg) then
			return self.PlaySkill(self,skill,target)	
		else
			if skill ~= nil and skill.info ~= nil and skill.info.type == 7 and self.character.commonTarget == nil then
				if self.character.enemyTeamData:GetCount() > 0 then
					self.character.mCommonTarget = self.character.enemyTeamData:GetCharacters()[0]
				end
			end
			self:PlaySkill(skill)
		end
		
	end
	if CS.GameData.dictTeamIdEnemyTeamInfo:ContainsKey(self.enemyTeamidUse) then
		self.enemyGroupInfo = CS.GameData.dictTeamIdEnemyTeamInfo[self.enemyTeamidUse]
	end
	if self.enemyGroupInfo ~= nil then
		for i = 0, self.enemyGroupInfo.Count -1 do
			--print (self.enemyGroupInfo[i].enemyTypeId)
			if self.enemyGroupInfo[i].enemyTypeId == 900308 or self.enemyGroupInfo[i].enemyTypeId == 900309 or
				self.enemyGroupInfo[i].enemyTypeId == 900310 or self.enemyGroupInfo[i].enemyTypeId == 900311 or
				self.enemyGroupInfo[i].enemyTypeId == 900313 then
				util.hotfix_ex(CS.BattleMemberController,'PlaySkill',PlaySkill)
				break
			end
			
		end
	end
	self:InitNormalBattle()
end
local OnDestroy = function(self)
	xlua.hotfix(CS.BattleMemberController,'PlaySkill',nil)
	self:OnDestroy()
end
util.hotfix_ex(CS.GF.Battle.BattleController,'InitNormalBattle',InitNormalBattle)
util.hotfix_ex(CS.GF.Battle.BattleController,'OnDestroy',OnDestroy)

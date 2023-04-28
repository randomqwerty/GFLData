local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleFieldTeamHolderNew)
xlua.private_accessible(CS.GF.Battle.BattleCharacterManager)
xlua.private_accessible(CS.GF.Battle.BattleMemberManager)
xlua.private_accessible(CS.GF.Battle.BattleManager)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)




local UpdateTargetsInRange = function(self,pos,skillCfg,createCfg)
	local flag = false
	if createCfg.effectAreaType == CS.GF.Battle.gsEffect.enumAffectArea.eCircle then
		if self.mResInRange == nil then
			self.mResInRange = CS.System.Collections.Generic.List(CS.GF.Battle.BattleCharacterManager)()
		else
			self.mResInRange:Clear()
		end
		local radius = CS.GF.Battle.SkillUtils.GetSkillPoolValue(skillCfg, createCfg.effectParam1)
		local angle = CS.TrueSync.FP(180)
		if createCfg.effectParam2 ~= 0 then
			angle  = CS.GF.Battle.SkillUtils.GetSkillPoolValue(skillCfg, createCfg.effectParam2)
		end
		local baseAngle = CS.TrueSync.TSVector2.right
		if angle < CS.TrueSync.FP(0) then
			angle = -angle
			baseAngle = CS.TrueSync.TSVector2.left
		end
		if angle == CS.TrueSync.FP(180) then
			flag = true
		end
		
		for i=0,self.listCharacter.Count-1 do
			local target = self.listCharacter[i]
			local myPos = CS.TrueSync.TSVector2(pos.x, pos.z)
			local targetPos = CS.TrueSync.TSVector2(target:GetWorldPosition().x, target:GetWorldPosition().z)
			
			
			if (CS.TrueSync.TSVector2.Distance(targetPos ,myPos) <= radius + self.UNIT_RADIUS ) and 
				(flag or VectorEquals(baseAngle,targetPos - myPos) or CS.TrueSync.TSVector2.Angle(baseAngle, targetPos - myPos) <= angle) then
				
				self.mResInRange:Add(target)
				
			else
				for j=0 ,target.listMember.Count-1 do
					local targetMemberPos = CS.TrueSync.TSVector2(target.listMember[j]:GetSelfPos(true).x, target.listMember[j]:GetSelfPos(true).z)
					if (CS.TrueSync.TSVector2.Distance(targetMemberPos ,myPos) <= radius + self.UNIT_RADIUS ) and 
						(flag or VectorEquals(baseAngle,targetMemberPos - myPos) or CS.TrueSync.TSVector2.Angle(baseAngle, targetMemberPos - myPos) <= angle) then
						
						self.mResInRange:Add(target)
						break
					end
				end
			end
			
		end
	else
		--print(createCfg.effectAreaType)
		self:UpdateTargetsInRange(pos,skillCfg,createCfg)
	end
end
VectorEquals = function(myPos,targetPos)
	
	local myPosNormal = myPos.normalized 
	local targetPosNormal = targetPos.normalized 
	local equalflag = (CS.TrueSync.FP.EqualFP(myPosNormal.x,targetPosNormal.x) and CS.TrueSync.FP.EqualFP(myPosNormal.y,targetPosNormal.y))
	return equalflag
end

local InitEnemyGroupInfo = function(self)
	self:InitEnemyGroupInfo()
	--print(CS.GF.Battle.BattleDynamicData.enemyTeamidUse)
	local enemyTeamidUse = CS.GF.Battle.BattleDynamicData.enemyTeamidUse
	if enemyTeamidUse == 942 or enemyTeamidUse == 1076 or enemyTeamidUse == 975
		or enemyTeamidUse == 1109 or enemyTeamidUse == 1405 or enemyTeamidUse == 1011
		or enemyTeamidUse == 700008 or enemyTeamidUse == 320901 or enemyTeamidUse == 930006
		or enemyTeamidUse == 1162 or enemyTeamidUse == 92157 or enemyTeamidUse == 1173
		or enemyTeamidUse == 590362 then
		
		util.hotfix_ex(CS.GF.Battle.BattleFieldTeamHolderNew,'UpdateTargetsInRange',UpdateTargetsInRange)
	else
		xlua.hotfix(CS.GF.Battle.BattleFieldTeamHolderNew,'UpdateTargetsInRange',nil)
	end
end
util.hotfix_ex(CS.GF.Battle.BattleManager,'InitEnemyGroupInfo',InitEnemyGroupInfo)

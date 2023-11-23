local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleController)
xlua.private_accessible(CS.GF.Battle.BattleCharacterManager)
xlua.private_accessible(CS.GF.Battle.BattleCharacterData)
xlua.private_accessible(CS.GF.Battle.BattleMemberData)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)
xlua.private_accessible(CS.GF.Battle.BattleMemberData)
xlua.private_accessible(CS.GF.Battle.CSkillInstance)
xlua.private_accessible(CS.GF.Battle.CharacterSkillImpl)
local FP = CS.TrueSync.FP
local GetBoneLocalPos = function(self,curFrame,boneName)
	local characterdata =  self.parentData
	if characterdata.isVehicleComponent or characterdata.isVehicle then
		print(characterdata.switchDistance)
		return self:GetBoneLocalPos(curFrame,boneName) * characterdata.switchDistance
	else
		return self:GetBoneLocalPos(curFrame,boneName)
	end
end
local Scout = function(self)
	local range = self.data.realtimeRange:AsFloat()
	if range <= 30 then
		return
	end
	self:Scout()
end
local DeathClear = function(self)
	
	self:DeathClear()
end
local GetBoneLocalPos = function(self,curFrame, boneName)
	local tempdir = self.curDir 
	if self.parentData.dir then
		self.curDir = not self.curDir
	end
	local result = self:GetBoneLocalPos(curFrame, boneName)
	self.curDir = tempdir
	return result
	
end
local Play = function(self,bTurnToDes)
	self:Play(bTurnToDes)
	if not self.mFinish then
		if self.mSelf:GetCharacterData() ~= nil then
			if self.mSelf:GetCharacterData().gunCode == "BossGager" then
				if self.mTargets.Count > 0 then
					self.mTargets[0].defPos = self.mTargets[0]:GetPos()
				end
			end
		end
		
	end
end
local _HandleScrEffectEvent = function(self,pEvent)
	
	if pEvent.ID == 5 or pEvent.ID == 8 then
		if self.mTargets.Count > 0 then
			self.mTargetPoses:Add(self.mTargets[0].defPos)
		end
	end
	self:_HandleScrEffectEvent(pEvent)
	if pEvent.ID == 5 or pEvent.ID == 8 then
		self.mTargetPoses:Clear()
	end
end
local CreateFriendlyCharacter = function(self)
	
	local v = self:CreateFriendlyCharacter()
	--if CS.GF.Battle.BattleDynamicData.isVehicleBattle then
	--	util.hotfix_ex(CS.GF.Battle.BattleMemberData,'GetBoneLocalPos',GetBoneLocalPos)
	--else
	--	xlua.hotfix(CS.GF.Battle.BattleMemberData,'GetBoneLocalPos',nil)
	--end
	print("")
	if CS.GF.Battle.BattleDynamicData.isRemoteBattle then
		util.hotfix_ex(CS.GF.Battle.BattleEnemyCharacterManager,'Scout',Scout)
	else
		xlua.hotfix(CS.GF.Battle.BattleEnemyCharacterManager,'Scout',nil)
	end
	if self.EntranceType == CS.BattleEntranceType.Theater then
		util.hotfix_ex(CS.GF.Battle.BattleCharacterManager,'DeathClear',DeathClear)
	else
		xlua.hotfix(CS.GF.Battle.BattleCharacterManager,'DeathClear',nil)
	end
	if CS.GF.Battle.BattleDynamicData.isSangvisBattle then
		util.hotfix_ex(CS.GF.Battle.BattleMemberData,'GetBoneLocalPos',GetBoneLocalPos)
	else
		xlua.hotfix(CS.GF.Battle.BattleMemberData,'GetBoneLocalPos',nil)
	end
	self.transform:Find("Canvas/DynamicCanvas/DPS").localPosition = CS.UnityEngine.Vector3(807,296.6,60)
	local enemyFlag = false
	local eList = CS.GF.Battle.BattleDynamicData.listEnemyCharacterDataAddlist
	if eList.Count > 0 then
		for i=0,eList.Count-1 do
			if eList[i]:GetGun().code == "BossGager" then
				enemyFlag = true
				break
			end
		end
	end
	if enemyFlag then
		util.hotfix_ex(CS.GF.Battle.CSkillInstance,'Play',Play)
		util.hotfix_ex(CS.GF.Battle.CSkillInstance,'_HandleScrEffectEvent',_HandleScrEffectEvent)
	else
		xlua.hotfix(CS.GF.Battle.CSkillInstance,'Play',nil)
		xlua.hotfix(CS.GF.Battle.CSkillInstance,'_HandleScrEffectEvent',nil)
	end
	return v
end

local NeedShowVehicleForwardBtn = function(self)
	local fp2 = FP.FromFloat(1.5)
	self.nearEnemyDistance = self.nearEnemyDistance - fp2
	local ans = self:NeedShowVehicleForwardBtn()
	self.nearEnemyDistance = self.nearEnemyDistance + fp2
	return ans
end

local CloseDeploymentMoni = function()
	if CS.GF.Battle.BattleController.renderTexture ~= nil then
		CS.GF.Battle.BattleController.renderTexture:Release();
	end
	CS.GF.Battle.BattleController.CloseDeploymentMoni();
end

local CheckTheaterEnemyTypeNum = function(self)
	self.DictEnemyTypeDieTimeStatistic = CS.GF.Battle.BattleDynamicData.DictEnemyTypeDieTimeStatistic
end
local ShowSkillPerformance= function(self,obj,e)
	self:ShowSkillPerformance(obj,e)
	if e.data.isFriendly then
		local character = self:GetControllerByData(e.data)
		if character ~= nil then
			character:PlaySkillVoice()
		end
	end
end
util.hotfix_ex(CS.GF.Battle.BattleController,'CreateFriendlyCharacter',CreateFriendlyCharacter)
util.hotfix_ex(CS.GF.Battle.BattleController,'NeedShowVehicleForwardBtn',NeedShowVehicleForwardBtn)
util.hotfix_ex(CS.GF.Battle.BattleController,'CloseDeploymentMoni',CloseDeploymentMoni)
util.hotfix_ex(CS.GF.Battle.BattleController,'CheckTheaterEnemyTypeNum',CheckTheaterEnemyTypeNum)
util.hotfix_ex(CS.GF.Battle.BattleController,'ShowSkillPerformance',ShowSkillPerformance)

local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleController)
xlua.private_accessible(CS.GF.Battle.BattleCharacterData)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)
xlua.private_accessible(CS.GF.Battle.BattleManager)
xlua.private_accessible(CS.GF.Battle.gsEffect)
xlua.private_accessible(CS.GF.Battle.BattleCharacterManager)
xlua.private_accessible(CS.GF.Battle.BattleFieldTeamHolderNew)
local FP = CS.TrueSync.FP


local CalcRemoteBattleEnemyRemainPercent= function(self)
	local listEnemyCharacterData = CS.GF.Battle.BattleDynamicData.listEnemyCharacterData
	for i = 0,listEnemyCharacterData.Count - 1 do
		local data = listEnemyCharacterData[i]
		data.bulletChainNum = data.startingLife
		data.startingLife = data.maxLife
		
	end
	
	self:CalcRemoteBattleEnemyRemainPercent()
	
	for i = 0,listEnemyCharacterData.Count - 1 do
		local data = listEnemyCharacterData[i]
		data.startingLife = data.bulletChainNum
		
	end
	local BattleDynamicData = CS.GF.Battle.BattleDynamicData
	if BattleDynamicData.enemyAllyTeam ~= nil then
		if BattleDynamicData.enemyAllyTeam.hpPercent <= 0 then
			BattleDynamicData.enemyAllyTeam.hpPercent = 0
		end
	else
		if BattleDynamicData.enemyTeamData ~= nil then
			if BattleDynamicData.enemyTeamData.hpPercent <= 0 then
				BattleDynamicData.enemyTeamData.hpPercent = 0
			end
		end
	end
	
end

local InitStartingPos = function(self)
	if self.isFriendly and (not self.isSummon) and (not self.isSquad) then
		local BattleDynamicData = CS.GF.Battle.BattleDynamicData
		for i=0,BattleDynamicData.listFriendlyGun.Count-1 do
			if self.gun == BattleDynamicData.listFriendlyGun[i] then
				self.index = i
				break
			end
		end	
	end
	self:InitStartingPos()
end
local NeedUploadAntiData = function(self)
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then 
		return false
	else
		return self:NeedUploadAntiData()
	end
end
local OutputAntiData = function(self,type)
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then 
		return
	else
		self:OutputAntiData(type)
	end
end

local CreateInst = function(self)
	self:CreateInst()
	if (self.m_bDie == false) and (self.mEffectCfg ~= nil) and (#self.mEffectCfg.code) > 0 then
		self.isInfoEffectObjExist = true
	end
end

local InitMemberOffset = function(self)
	self:InitMemberOffset()
	if self.data.camp == CS.GF.Battle.Camp.friendly and self.data.isVehicleComponent == false and self.data.isSummon == false then
		if self.listMember.Count == 1 then
			self.listMember[0].localPosition = self.listMember[0].localPosition + CS.TrueSync.TSVector(FP.FromFloat(0.35),FP.FromFloat(0),FP.FromFloat(0))
		end
	end
end

local InitSpotActionByEntrance = function(self)
	local BattleDynamicData = CS.GF.Battle.BattleDynamicData
	local flag = true
	self:InitSpotActionByEntrance()
	if BattleDynamicData.EntranceType == CS.BattleEntranceType.Normal then
		if BattleDynamicData.currentSpotAction.spotInfo.id == 11468 or BattleDynamicData.currentSpotAction.spotInfo.id == 12504 then
			util.hotfix_ex(CS.GF.Battle.gsEffect,'CreateInst',CreateInst)
			util.hotfix_ex(CS.GF.Battle.BattleCharacterManager,'InitMemberOffset',InitMemberOffset)
			flag = false
		end
	end
	if flag then
		xlua.hotfix(CS.GF.Battle.gsEffect,'CreateInst',nil)
		xlua.hotfix(CS.GF.Battle.BattleCharacterManager,'InitMemberOffset',nil)
	end
end
local CreateFriendlyCharacterManager = function()
	local BattleDynamicData = CS.GF.Battle.BattleDynamicData
	if BattleDynamicData.EntranceType == CS.BattleEntranceType.SangvisCapture then
		for i=0,BattleDynamicData.listFriendlyGun.Count-1 do
			local gun = BattleDynamicData.listFriendlyGun[i]
			if gun ~= nil and gun.life > 0 then
				if BattleDynamicData.isSingleBattleMode then
					gun:ConvertToSingleMode()
				end
				local characterManager
				if gun:GetType() == typeof(CS.SangvisGun) then
					characterManager = CS.GF.Battle.BattleSangvisCharacterManager()
				else
					characterManager = CS.GF.Battle.BattleFriendlyCharacterManager()
				end
				characterManager:Init(gun, CS.GF.Battle.Camp.friendly, i)
				BattleDynamicData.friendlyTeamHolder:AddCharacter(characterManager)
			end
		end
	else
		BattleDynamicData.CreateFriendlyCharacterManager()
	end
end
util.hotfix_ex(CS.GF.Battle.BattleManager,'CalcRemoteBattleEnemyRemainPercent',CalcRemoteBattleEnemyRemainPercent)
util.hotfix_ex(CS.GF.Battle.BattleManager,'InitSpotActionByEntrance',InitSpotActionByEntrance)
util.hotfix_ex(CS.GF.Battle.BattleCharacterData,'InitStartingPos',InitStartingPos)
util.hotfix_ex(CS.GF.Battle.BattleManager,'NeedUploadAntiData',NeedUploadAntiData)
util.hotfix_ex(CS.GF.Battle.BattleController,'OutputAntiData',OutputAntiData)
util.hotfix_ex(CS.GF.Battle.BattleDynamicData,'CreateFriendlyCharacterManager',CreateFriendlyCharacterManager)
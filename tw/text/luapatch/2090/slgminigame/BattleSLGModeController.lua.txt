local util = require 'xlua.util'
local config = require ('2090/SLGMinigame/BattleSLGModeConfig')
xlua.private_accessible(CS.GF.Battle.BattleSLGModeController)
xlua.private_accessible(CS.GF.Battle.BattleCharacterController)
xlua.private_accessible(CS.BattleSLGUIController)
local flatSkillCancelFlag = false
local flatSkillCancelCounter = 0
local tempPos = 0
local coveredEfectCode = "Effect/Zhishi_tietu"
local coveredEfectObj
local battleController = CS.GF.Battle.BattleController
local Init = function(self)
	self.curStageNum = self:GetStageNum()
	config:InitData(self.curStageNum)
	tempPos = 0
	CS.GF.Battle.BattleSLGModeController.gridwidth = gridwidth
	CS.GF.Battle.BattleSLGModeController.gridheight = gridheight
	CS.GF.Battle.BattleSLGModeController.gridHorizontalAmount = gridHorizontalAmount[self.curStageNum]
	CS.GF.Battle.BattleSLGModeController.gridVerticalAmount = gridVerticalAmount
	CS.GF.Battle.BattleSLGModeController.resourcePointMax = resourcePointMax[self.curStageNum]
	CS.GF.Battle.BattleSLGModeController.RPRengenTimeFrame = RPRengenTimeFrame
	self.resourcePointMoveCost  =resourcePointMoveCost
	self.startingResourcePoint = startingResourcePoint[self.curStageNum]
	self.friendlyAreaOffset = friendlyAreaOffset
	self.CameraStaticOffset = CameraStaticOffset
	self.camaraStaticRotation = camaraStaticRotation
	self:Init()
	
end
local RequestSLGSkillWithoutTarget = function(self,caster,skillid)
	
	if self:RequestSLGSkillWithoutTarget(caster,skillid) then
		self:CancelCurrentSelSLGSkill()
		CS.BattleSLGUIController.Instance:ShowSLGSelectTargetUI(skillid)	
		CS.BattleSLGUIController.Instance.btnCancelCastSkill.gameObject:SetActive(false)
		flatSkillCancelFlag = true
		return true
	else
		return false	
	end
end

local RequestSLGSkillSelectTarget = function(self,caster,skillid)
	if self.SLGSkillSelectingTarget and self.curCaster ~= nil and self.curConfig ~= nil and caster == self.curCaster and self.curConfig.skillid == skillid then
		return
	end
	CS.BattleSLGUIController.Instance.btnCancelCastSkill.gameObject:SetActive(true)
	self:RequestSLGSkillSelectTarget(caster,skillid)
	
end
local MainLoop = function(self)
	if flatSkillCancelFlag then
		flatSkillCancelCounter = flatSkillCancelCounter + 1
		if flatSkillCancelCounter >= 60 then
			flatSkillCancelFlag = false
			flatSkillCancelCounter = 0
			if not self.SLGSkillSelectingTarget then
				CS.BattleSLGUIController.Instance:ShowNormalUI()
			end
		end
	end
	if self.frontlineCharacter == nil and self.autoFocusChara ~= nil then
		self.frontlineCharacter = self.autoFocusChara	
		CS.BattleInteractionController.dragOffset = CS.UnityEngine.Vector2(self:GetFrontlineFriendlyCharacterPos() * gridwidth,CS.BattleInteractionController.dragOffset.y) 
	end
	self:MainLoop()
end
local RequestCastSkill = function(self,skill,isSp,checkBuff)
	local slgConfig = self.battleSLGMinigameSkillCfgs:GetDataById(skill.info.id)
	if slgConfig ~= nil then
		if not isSp then
			if self.CurrentSelectCharacter ~= nil and not self.CurrentSelectCharacter:IsDead() then
				if checkBuff then
					if self.CurrentSelectCharacter:GetSLGAttackChargeBuffNumber() > 0 then
						if self:GetCharacterCoveredStatus(self.CurrentSelectCharacter) then
							local alterSkill = self.CurrentSelectCharacter.gun:GetSkillByGroupId(skill.id + 100)
							if alterSkill ~= nil then
								self.CurrentSelectCharacter.listMember[0]:RequestCastSLGSkill(alterSkill, skill);
								return
							end
						end
					end
				end
			end
		end
	end
	self:RequestCastSkill(skill,isSp,checkBuff)
end
local GetCharacterCoveredStatus = function(self,chara)
	if (chara.conditionListSelf:GetTierByID(4650)> 0) then
		return true
	else
		return self:GetCharacterCoveredStatus(chara)
	end
end
local LoadDataFromLocal = function(self)
	--self:LoadDataFromLocal()
	self.inited = false
end
local GetStageNum = function(self)
	local enemyNum =CS.GameData.engagedSpot.enemyTeamId
	for i=1,#minigameEnemyGroupID do
		if enemyNum == minigameEnemyGroupID[i] then
			return i		
		end
	end
	return 1
end
local LoadStageData = function(self)
	
	
	for i=1,#minigameEnemyGroupID do
		local stageConfig  = CS.GF.Battle.BattleSLGStageConfig(i,stageStrategyGunID[i])
		for j=1,#stageStrategySkills[i] do
			stageConfig:AddStrategySkill(stageStrategySkills[i][j])
		end
		self.battleSLGMinigameStageCfgs:Add(stageConfig)
	end
end
local LoadSLGSkillData = function(self)
	for i=1,#SLGSkills do
		local skillconfig = SLGSkills[i]
		self.battleSLGMinigameSkillCfgs:Add(CS.BattleSLGMinigameSkillCfg(skillconfig.skillid,skillconfig.skillrange,skillconfig.skilltype,skillconfig.skillcost,skillconfig.spcost))
	end
	
end
local LoadSLGEnemyData= function(self)
	local startingpoint = CS.UnityEngine.Vector2Int(0,0)
	for i=0,#SLGEnemyMoves do
		local localConfig = SLGEnemyMoves[i]
		local enemyConfig =CS.BattleSLGMinigameEnemyCfg(localConfig.id,not localConfig.isMove,startingpoint)
		enemyConfig.isLoop = localConfig.isLoop
		if localConfig.movePoints~= nil then
			for j=1,#localConfig.movePoints do	
				if 	#localConfig.waitFrames < j then
					enemyConfig:AddPoint(localConfig.movePoints[j].x-1,localConfig.movePoints[j].y-1,0)
				else
					enemyConfig:AddPoint(localConfig.movePoints[j].x-1,localConfig.movePoints[j].y-1,localConfig.waitFrames[j])
				end

			end
		end
		self.battleSLGMinigameEnemyCfgs:Add(enemyConfig)
	end
end

local LoadSLGEnemyGroupInfo = function(self)
	for i=1,#SLGEnemyGroupData do
		if SLGEnemyGroupData[i].id == self.curStageNum then
			local enemydata = SLGEnemyGroupData[i]
			local emptyList = CS.System.Collections.Generic["List`1[System.Int32]"]()
			--print(SLGEnemyGroupData[i].id..' '..#enemydata.moveGroup)
			for j=1,#enemydata.moveGroup do
				emptyList:Add(enemydata.moveGroup[j])
			end
			self.dictSLGMinigameEnemyGroupInfo:Add(enemydata.enemyGroupid,emptyList)
			break
		end
	end
end
local LoadFriendlyStartingData = function(self)
	for i=1,#friendlyStartingPos do
		self.battleSLGFriendlyCharacterStartingPos:Add(CS.UnityEngine.Vector2Int(friendlyStartingPos[i].x-1,friendlyStartingPos[i].y-1))
	end
end
local ChangeRPoint = function(self,num)
	if num == 0 then return end
	self:ChangeRPoint(num)
end

local RemoveCharacter = function(self,chara)
	local lastpos
	local flag = false
	if self.dictCharacterPosition:ContainsKey(chara) then
		lastpos = self.dictCharacterPosition[chara]
		flag = true
	end
	self:RemoveCharacter(chara)
	local friendlyCharacters = battleController.Instance.friendlyTeamHolder:GetCharacters()
	if flag then
		for i=0,friendlyCharacters.Count-1 do
			if not friendlyCharacters[i]:IsDead() and self.dictCharacterPosition:ContainsKey(friendlyCharacters[i]) then
				if self.dictCharacterPosition[friendlyCharacters[i]] == lastpos then
					self.dictGridInfo[lastpos].friendlyCharacter = friendlyCharacters[i]
					break
				end
			end
		end 
	end
	if self.CurrentSelectCharacter == chara then
		self.CurrentSelectCharacter = nil		
		for i=0,friendlyCharacters.Count-1 do
			if not friendlyCharacters[i]:IsDead() and self.dictCharacterPosition:ContainsKey(friendlyCharacters[i]) then
				self:OnSelectFriendlyCharacter(friendlyCharacters[i])
				break
			end
		end
	end
end

local GetFrontlineWidth = function(self)

	if self.curStageNum == 3 or self.curStageNum == 4 then
		return 26.2
	end
	local nowPos = self:GetFrontlineFriendlyCharacterPos() * gridwidth + self.camFrontlineExtraRange
	if nowPos > tempPos then
		tempPos = nowPos
	end
	return tempPos
end
local TryCastSkill = function(self,target,targetpos)
	self:TryCastSkill(target,targetpos)
	if self.curConfig ~= nil then
		if not self:CheckSpCost(self.curCaster,self.curConfig.spcost) then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(10193))
		end
	end
end
local EnemyCharacterMoveTo = function(self,chara,newpos)
	self:EnemyCharacterMoveTo(chara,newpos)
	chara.mCommonTarget = nil
	chara:SLGScout()
end
local CharacterMoveTo = function(self,chara,newpos)
	local lastpos = self.dictCharacterPosition[chara]
	self:CharacterMoveTo(chara,newpos)
	local friendlyCharacters = battleController.Instance.friendlyTeamHolder:GetCharacters()
	for i=0,friendlyCharacters.Count-1 do
		if not friendlyCharacters[i]:IsDead() and self.dictCharacterPosition:ContainsKey(friendlyCharacters[i]) then
			if self.dictCharacterPosition[friendlyCharacters[i]] == lastpos then
				self.dictGridInfo[lastpos].friendlyCharacter = friendlyCharacters[i]
				break
			end
		end
	end
end
local blockpos
local effectObj
local effectTransformParent
local RefreashShelterStatus = function(self)
	self:RefreashShelterStatus()
	coveredEfectObj = CS.ResManager.GetObjectByPath(coveredEfectCode)
	effectTransformParent = CS.GF.Battle.BattleController.Instance.friendlyTeamHolder.transform
	local dic = self.dictGridInfo
	for k,v in pairs(dic) do
		if v.isCovered then
			blockpos = self:GetPositionFromGrid(k)
			effectObj = CS.UnityEngine.Object.Instantiate(coveredEfectObj)
			effectObj.gameObject.transform:SetParent(effectTransformParent,false)
			effectObj.gameObject.transform.localPosition = blockpos
		end
	end
	coveredEfectObj = nil
	effectObj = nil
	effectTransformParent = nil
end
util.hotfix_ex(CS.GF.Battle.BattleSLGModeController,'Init',Init)
util.hotfix_ex(CS.GF.Battle.BattleSLGModeController,'RequestSLGSkillWithoutTarget',RequestSLGSkillWithoutTarget)
util.hotfix_ex(CS.GF.Battle.BattleSLGModeController,'RequestSLGSkillSelectTarget',RequestSLGSkillSelectTarget)
util.hotfix_ex(CS.GF.Battle.BattleSLGModeController,'MainLoop',MainLoop)
util.hotfix_ex(CS.GF.Battle.BattleSLGModeController,'GetCharacterCoveredStatus',GetCharacterCoveredStatus)
util.hotfix_ex(CS.GF.Battle.BattleSLGModeController,'RequestCastSkill',RequestCastSkill)
util.hotfix_ex(CS.GF.Battle.BattleSLGModeController,'LoadDataFromLocal',LoadDataFromLocal)
util.hotfix_ex(CS.GF.Battle.BattleSLGModeController,'ChangeRPoint',ChangeRPoint)
util.hotfix_ex(CS.GF.Battle.BattleSLGModeController,'RemoveCharacter',RemoveCharacter)
util.hotfix_ex(CS.GF.Battle.BattleSLGModeController,'GetFrontlineWidth',GetFrontlineWidth)
util.hotfix_ex(CS.GF.Battle.BattleSLGModeController,'RefreashShelterStatus',RefreashShelterStatus)
util.hotfix_ex(CS.GF.Battle.BattleSLGModeController,'TryCastSkill',TryCastSkill)
util.hotfix_ex(CS.GF.Battle.BattleSLGModeController,'EnemyCharacterMoveTo',EnemyCharacterMoveTo)
util.hotfix_ex(CS.GF.Battle.BattleSLGModeController,'CharacterMoveTo',CharacterMoveTo)
xlua.hotfix(CS.GF.Battle.BattleSLGModeController,'GetStageNum',GetStageNum)
xlua.hotfix(CS.GF.Battle.BattleSLGModeController,'LoadStageData',LoadStageData)
xlua.hotfix(CS.GF.Battle.BattleSLGModeController,'LoadSLGSkillData',LoadSLGSkillData)
xlua.hotfix(CS.GF.Battle.BattleSLGModeController,'LoadSLGEnemyData',LoadSLGEnemyData)
xlua.hotfix(CS.GF.Battle.BattleSLGModeController,'LoadSLGEnemyGroupInfo',LoadSLGEnemyGroupInfo)
xlua.hotfix(CS.GF.Battle.BattleSLGModeController,'LoadFriendlyStartingData',LoadFriendlyStartingData)
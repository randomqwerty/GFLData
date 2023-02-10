local util = require 'xlua.util'
local config = require ('Battle/3010/2022ScarMinigameConfig')
local util = require 'xlua.util'
xlua.private_accessible(CS.CommonAudioController)
xlua.private_accessible(CS.CommonController)
xlua.private_accessible(CS.ResManager)
xlua.private_accessible(CS.BattleManualSkillController)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)
xlua.private_accessible(CS.GF.Battle.BattleCharacterControllerNew)
xlua.private_accessible(CS.GF.Battle.BattleMemberControllerNew)
xlua.private_accessible(CS.GF.Battle.BattleFieldTeamHolderNew)
xlua.private_accessible(CS.GF.Battle.BattleController)
xlua.private_accessible(CS.GF.Battle.BattleManager)
xlua.private_accessible(CS.GF.Battle.BattleStatistics)
xlua.private_accessible(CS.GF.Battle.BattleFrameTimer)
xlua.private_accessible(CS.BattleUIPauseController)
xlua.private_accessible(CS.GF.Battle.BattleConditionList)
xlua.private_accessible(CS.GF.Battle.CharacterCondition)
xlua.private_accessible(CS.GF.Battle.EffectManager)
xlua.private_accessible(CS.GF.Battle.BattleFairyData)
xlua.private_accessible(CS.GF.Battle.BattleFriendlyCharacterManager)


local character = nil
local characterData
local mCurSkill ={}
local maxX = 5
local minX = -1
local maxY = 4
local minY = -5.6
local txCD = nil
--X分量的系数
local speedXPara = 0.02
--Y分量的系数
local speedYPara = 0.02
--后撤移动时的额外系数
local cfgMoveFoward = nil
local cfgMoveBack = nil
local isMoving = false
local thisFrameJoyStick = false
local timecount = 0
local textTime
local CountTime = true
local BattleController
local friendlyArea
local friendlyAreaInitalPos
local lifebarFlag = false
local lifebarFlag2 = false
local FP = CS.TrueSync.FP

local SkillUtils = CS.GF.Battle.SkillUtils

local animDuration = 4
local animDelay = 2
local animTimer = 4

local gameStartAnimFlag = false
local gameEndAnimFlag = false
local cannotMoveFlag = false

local gameStartBuffID  = 4585
local gameEndBuffID  = 4586
local cannotMoveBuffID  = 4587
local layerBuffID = 4851
local timingBuffID = 4869

local cooldownTween
local cooldownImage

local btnFadeInLeftDelay = 0.5
local btnFadeInRightDelay = 0.5
local lifebarFadeInDelay = 0.5

local btnFadeInLeftDuration = 4
local btnFadeInRightDuration = 6
local lifebarFadeInDuration = 4

local spineVisionFarDelay = 0
local spineVisionNearDelay = 0

local blackBGDelay = 4.8
local blackBGTimer = 0
local blackBGMoveSpeed = 100
local blackBGMoveUpperBound = 800
local blackBGMoveLowerBound = -800

local startAnimSkillAction = 11762101
local moveSoundInterval = 0.8
local moveSoundFrameTimer = 4

local backGround
local backGroundFloor
local backGroundWall
local showDialogue = false

--local gunCode = "M9"
local tempvalue = 0
local effectWall
local effectFloor
--local effectWallPos = {0,4.2,20.75}
--local effectWallRot = {10,0,0}
--local effectWallScale = {1,1,1}

--local effectFloorPos = {0,1.26,-5.06}
--local effectFloorRot = {90,0,0}
--local effectFloorScale = {0.4,1.57,0.6}
--local baseRate = 50
--local effectWallMoveCoef = 0.9
--local effectFloorMoveCoef = 0.48
local lerpCoef = 0.6
local timer = 0
local lastValue = 0.5

local EnemyIDNormal = 6560401
local EnemyIDHard = 6561401

local skillid1 = 11980201
local skillid2 = 11980301
local _skillLabel1
local _skillLabel2
local Mathf = CS.UnityEngine.Mathf
local isPlayingEndingAnim = false
local waitAVG = false
local endingAnimTimer = 0
local isGameEnd = false
local isActionPlayed = false
--local addNum = 4

local targetBuff
local startFlag = false

local characterTransform
local enemyTransform
local characterStartingPos
local enemyStartingPos
local BattleDynamicData = CS.GF.Battle.BattleDynamicData

InitSkill1 = function(SkillLabel,mCurSkill,pos)
	local skillLabelController
	skillLabelController = SkillLabel:GetComponent(typeof(CS.BattleManualSkillController))
	--注册技能和人物
	skillLabelController.mCurChar = characterData
	skillLabelController.mCurSkill = mCurSkill
	--初始化
	if pos == 1 then
		skillLabelController.imgBgActive.sprite = skillLabelController.arrSprBg[0]
		skillLabelController.imgBgActive.transform.localScale = CS.UnityEngine.Vector3(-1, 1, 1)
		skillLabelController.imgBgDisable.sprite = skillLabelController.arrSprBg[0]
		skillLabelController.imgBgDisable.transform.localScale = CS.UnityEngine.Vector3(-1, 1, 1)
		skillLabelController.imgBgPassive.sprite = skillLabelController.arrSprBg[0]
		skillLabelController.imgBgPassive.transform.localScale = CS.UnityEngine.Vector3(-1, 1, 1)
		skillLabelController.imageHintBg.transform.localScale = CS.UnityEngine.Vector3(-1, 1, 1)
	end
	if pos == 2 then
		skillLabelController.imgBgActive.sprite = skillLabelController.arrSprBg[0]
		skillLabelController.imgBgActive.transform.localScale = CS.UnityEngine.Vector3(1, 1, 1)
		skillLabelController.imgBgDisable.sprite = skillLabelController.arrSprBg[0]
		skillLabelController.imgBgDisable.transform.localScale = CS.UnityEngine.Vector3(1, 1, 1)
		skillLabelController.imgBgPassive.sprite = skillLabelController.arrSprBg[0]
		skillLabelController.imgBgPassive.transform.localScale = CS.UnityEngine.Vector3(1, 1, 1)
		skillLabelController.imageHintBg.transform.localScale = CS.UnityEngine.Vector3(1, 1, 1)
	end
	skillLabelController.imageRank.sprite = skillLabelController.spriteRarity[characterData.gun.info.rank]
	skillLabelController.imageIcon.enabled = false
	skillLabelController.imageIcon:GetComponent(typeof(CS.UnityEngine.RectTransform)).sizeDelta = CS.UnityEngine.Vector2(120, 120)
	skillLabelController.imageIcon:GetComponent(typeof(CS.UnityEngine.UI.RectMask2D)).enabled = true
	local pic = CS.CommonController.LoadSmallPic(characterData.gun, skillLabelController.imageIcon.transform, CS.UnityEngine.Vector2.zero)
	if pic ~= nil then
		pic:ShowTuJian(nil, 0.4, 0.6)
		local transPic = pic:GetComponent(typeof(CS.UnityEngine.RectTransform))
		transPic.localScale = CS.UnityEngine.Vector3(0.75, 0.3, 1)
		transPic.anchoredPosition = CS.UnityEngine.Vector2(0, 18)
	end
	skillLabelController.imageIcon.gameObject:SetActive(true)
	skillLabelController.goSkill2Perf:SetActive(false)
	skillLabelController.animCDDone.gameObject:SetActive(false)
	skillLabelController.animActive.gameObject:SetActive(false)
	skillLabelController.imageHintBg.gameObject:SetActive(false)
	if mCurSkill ~= nil then
		--print("-----------"..pos)
		local skillIcon = CS.CommonController.InstantiateSkillIcon(mCurSkill.info:GetIconCodeBySkin(characterData.gun.currentSkinId))
		local rectIcon = skillIcon:GetComponent(typeof(CS.UnityEngine.RectTransform))
		rectIcon:SetParent(skillLabelController.objSkill.transform,false)
		rectIcon:SetSiblingIndex(0)
		rectIcon:SetSizeWithCurrentAnchors(CS.UnityEngine.RectTransform.Axis.Horizontal, 100)
		rectIcon:SetSizeWithCurrentAnchors(CS.UnityEngine.RectTransform.Axis.Vertical, 100)
	end
	skillLabelController:_Active(true)
end
JoyStickMove = function(input)
	thisFrameValue = input
	
	if input.value <= 0 then
		thisFrameJoyStick = false
		return
	end
	thisFrameJoyStick = true
	
end

JoyStickBegin = function(input)
	
end

JoyStickEnd = function(input)
	
end

TriggerInvincible = function()
	
end
UpdateArmySpeed = function()
	
end
--Awake：初始化数据
Awake = function()
	-- 关闭自动释放技能
	--textTime = TextTime:GetComponent(typeof(CS.ExText))

	BattleDynamicData.infiScoutDistance = true
	local CheckBaseLine = function(self)
		if (self:CheckAllIsPhased(BattleDynamicData.enemyTeamHolder.listCharacter)) then
			self:BattleFinishAction(false)
			return
		end
		if (self:CheckAllIsPhased(BattleDynamicData.friendlyTeamHolder.listCharacter)) then
			self:BattleFinishAction(false)
			return
		end
	end
	local OnPointerDown = function(self,eventData)
		self:_Active(false,false)
		--print(self.mCurSkill.info.id..' '..skillid1..' '..skillid2)
		if self.mCurSkill.info.id == skillid1 then
			--startFlag = true
			PlaySFX("button")
			if targetBuff ~= nil then
				targetBuff.num = targetBuff.num + addNum
			else
				CS.GF.Battle.SkillUtils.GenBuffViaSkillConfig(characterData,skillid1,{addNum})
			end
			
		end
		if self.mCurSkill.info.id == skillid2 then
			CS.GF.Battle.SkillUtils.GenBuffViaSkillConfig(characterData,skillid2,{1})
		end
	end
	local OnPointerUp = function(self,eventData)
		self:_Active(true,false)
	end
	local Init = function(self,gun,camp,index,issummon,sdata)
		self:Init(gun,camp,index,issummon,sdata)
		if not issummon then
			self.characterData.isOutOfAMMO = true
			self.characterData.characterPosition = CS.UnityEngine.Vector3(-1000,0,0).ToTSVector()
			--self.transform.localPosition = CS.UnityEngine.Vector3(-1000,0,0)
		end
	end
	local DisableRangeLine = function(self)
		return true
	end
	local SetFairyData = function(self,fairy)
		local friendlyFairyData = CS.GF.Battle.BattleFairyData()
		friendlyFairyData:Init(CS.Fairy(CS.Data.GetFakeFairyInfo()))
		self:SetFairyData(friendlyFairyData)
	end
	--util.hotfix_ex(CS.GF.Battle.BattleController,'RefreshFriendlyTargetList',RefreshFriendlyTargetList)
	util.hotfix_ex(CS.GF.Battle.BattleManager,'CheckBaseLine',CheckBaseLine)
	util.hotfix_ex(CS.BattleManualSkillController,'OnPointerDown',OnPointerDown)
	util.hotfix_ex(CS.BattleManualSkillController,'OnPointerUp',OnPointerUp)
	util.hotfix_ex(CS.GF.Battle.BattleFriendlyCharacterManager,'Init',Init)
	util.hotfix_ex(CS.BattleInteractionController,'DisableRangeLine',DisableRangeLine)
	util.hotfix_ex(CS.GF.Battle.BattleFairyController,'SetFairyData',SetFairyData)
	--if CS.CommonAudioController.Instance.bgmSource ~= nil then
	--	CS.CommonAudioController.Instance.bgmSource:Stop()
	--end
	
end
local haloObj


--Start: 加载组件
Start = function()
	--禁止人物拖动
	--CS.BattleScaler.maxNumber = 5
	CS.GF.Battle.BattleScaler.InitScalerByMaxNum(0)
	BattleController = CS.GF.Battle.BattleController.Instance
	CS.BattleInteractionController.isGuideInteractable = false
	CS.BattleInteractionController.isGuideCanNotScale = false
	CS.BattleInteractionController.isGuideCanNotOffset = false
	CS.GF.Battle.SkillUtils.AutoSkill = false	
	BattleController.resetAutoSkill = true
	BattleController.resetCameraLock = true
	--BattleController.transform:Find("BattleField/CameraPositionDynamic/CameraPositionStatic/Main Camera/ShiningDust").gameObject:SetActive(false)
	haloObj = BattleController.transform:Find("Canvas/Halo").gameObject
	--haloObj:SetActive(false)
	backGround = BattleController.transform:Find("BattleField/scarbossbattle(Clone)").gameObject
	backGroundFloor = backGround.transform:Find("地面").gameObject:GetComponent(typeof(CS.UnityEngine.MeshRenderer)).material
	backGroundWall = backGround.transform:Find("近景").gameObject:GetComponent(typeof(CS.UnityEngine.MeshRenderer)).material
	BattleController.transform:Find("Canvas/UI/SafeUIRect/DPSSwitch").gameObject:SetActive(false)
	BattleController.transform:Find("Canvas/DynamicCanvas/DPS").gameObject:SetActive(false)
	BattleController.transform:Find("Canvas/UI/Top/Top_Time").gameObject:SetActive(false)
	
	--self:GetComponent('Canvas').worldCamera = CS.UnityEngine.Camera.main
	--注册人物
	
	if friendlyArea == nil then
		friendlyArea = BattleController.friendlyArea
		friendlyAreaInitalPos = friendlyArea.localPosition.x
	end
	
	
	--mCurSkill[2] = character.gun:GetSkillByGroupId(406611)
	-- 人物扶正
	--character.listMember[0].transform.localEulerAngles = CS.UnityEngine.Vector3(0, 0, 0)
	
	-- 关闭自动技能 --------打完要记得调回去！（LoadAutoSkillPref）---------
	
	--countDown:GetComponent('Transform')
	--BtnTest:GetComponent('Button').onClick:AddListener(TestFunc)
	
	CS.BattleLuaUtility.SwitchUIManualPannel(false,false) -- 关闭手动技能面板
	
	--CS.BattleFrameManager.Register(UpdateJoyStick)
	--JoyStick:GetComponent(typeof(CS.Joystick)).JoystickMoveHandle = JoyStickMove
	--JoyStick:GetComponent(typeof(CS.Joystick)).JoystickEndHandle = JoyStickEnd
	--JoyStick:GetComponent(typeof(CS.Joystick)).JoystickBeginHandle = JoyStickBegin
	
	
	
	effectWall = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Effect/Dance_uv"))
	effectWall.transform:SetParent(BattleController.holderCreation,false)
	effectWall.transform.localPosition = CS.UnityEngine.Vector3(effectWallPos[1],effectWallPos[2],effectWallPos[3])
	effectWall.transform.localRotation= CS.UnityEngine.Quaternion.Euler(effectWallRot[1],effectWallRot[2],effectWallRot[3])
	effectWall.transform.localScale = CS.UnityEngine.Vector3(effectWallScale[1],effectWallScale[2],effectWallScale[3])
	
	effectFloor = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Effect/Dance_uv"))
	effectFloor.transform:SetParent(BattleController.holderCreation,false)
	effectFloor.transform.localPosition = CS.UnityEngine.Vector3(effectFloorPos[1],effectFloorPos[2],effectFloorPos[3])
	effectFloor.transform.localRotation= CS.UnityEngine.Quaternion.Euler(effectFloorRot[1],effectFloorRot[2],effectFloorRot[3])
	effectFloor.transform.localScale = CS.UnityEngine.Vector3(effectFloorScale[1],effectFloorScale[2],effectFloorScale[3])
	local camarapos = BattleController.transform:Find("BattleField/CameraPositionDynamic/CameraPositionStatic").gameObject
	camarapos.transform.localPosition = CS.UnityEngine.Vector3(camarapos.transform.localPosition.x,3.5,camarapos.transform.localPosition.z)
	camarapos.transform.localRotation= CS.UnityEngine.Quaternion.Euler(10,0,0)
	--txCD = goCD:GetComponent('Text');
	
	--BtnShimmer:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
	--	function()
	--		ManualActiveSkill(mCurSkill[1])
	--	end)
	--if not gameStartAnimFlag then
	--	JoyStick:SetActive(false)
	--	--BtnShimmer:SetActive(false)
	--end
	--注册相机
	
	self.transform:SetParent(CS.BattleUIController.Instance.transform:Find('UI'),false)
	--self.transform.localPosition = CS.BattleUIManualSkillController.Instance.transform.localPosition
	--SkillLabel1.transform.localPosition = CS.UnityEngine.Vector3(SkillLabel1.transform.localPosition.x,89,SkillLabel1.transform.localPosition.z)
	--SkillLabel2.transform.localPosition = CS.UnityEngine.Vector3(SkillLabel2.transform.localPosition.x,89,SkillLabel2.transform.localPosition.z)
	PlaySFX("loop")
end
InitCharacter = function()
	print("InitCharacter")
	character.reverseSync = true
	characterData = character.data 
	local charPos = character.transform
	lifebarOffset = character.listMembers[0].transform.localPosition
	character.listMembers[0].transform.localPosition = CS.UnityEngine.Vector3.zero
	character.listMembers[0].mesh.sortingOrder = 3
	_skillLabel1 = SkillLabel1:GetComponent(typeof(CS.BattleManualSkillController))
	--_skillLabel2 = SkillLabel2:GetComponent(typeof(CS.BattleManualSkillController))
	--character:SetMemberAnimation("wait", 1)
	--注册人物技能
	mCurSkill[1] = characterData:GetSkillByID(119802,true)
	mCurSkill[2] = characterData:GetSkillByID(119803,true)
	InitSkill1(_skillLabel1,mCurSkill[1],1)
	--InitSkill1(_skillLabel2,mCurSkill[2],2)
	characterTransform = character.gameObject.transform
	--local enemyCharacterData = BattleDynamicData.enemyTeamHolder.listCharacter[0]
	local enemyCharacter = BattleController.listEnemyCharacterControllers[0]
	enemyCharacter.reverseSync = true
	enemyTransform =  enemyCharacter.gameObject.transform
	enemyTransform.position = CS.UnityEngine.Vector3(enemyTransform.position.x,enemyTransform.position.y,characterTransform.position.z)
	characterStartingPos = character.transform.localPosition
	enemyStartingPos = enemyTransform.localPosition
end

Update = function()
	
	timer = timer + (CS.UnityEngine.Time.deltaTime) * lerpCoef
	--tempvalue = tempvalue -0.3
	if friendlyArea ~= nil then
		local offset = friendlyArea.localPosition.x - friendlyAreaInitalPos
		local offsetFP = FP.FromFloat(offset)
		CS.GF.Battle.BattleDynamicData.friendlyArmyOffset = offsetFP
	end
	if haloObj ~= nil and haloObj.activeSelf then
		haloObj:SetActive(false)
	end
	if character == nil then
		character = CS.BattleLuaUtility.GetCharacterControllerNewByCode(gunCode)
		if character == nil then	
			return
		else
			InitCharacter()
		end 
	end
	if targetBuff == nil then
		
		for i=0,characterData.conditionListSelf.mListCondition.Count-1 do
			if characterData.conditionListSelf.mListCondition[i].id == layerBuffID then
				targetBuff = characterData.conditionListSelf.mListCondition[i]
				break
			end
		end
	end
	
	--UpdateEnemyState()
	--UpdateCreationState()
	if not lifebarFlag and character.lifeBar ~= nil then
		character.lifeBar.gameObject:SetActive(false)
		lifebarFlag = true
	end
	if not lifebarFlag2 and BattleController.enemyTeamHolder:GetCharacters()[0].lifeBar ~= nil then
		BattleController.enemyTeamHolder:GetCharacters()[0].lifeBar.gameObject:SetActive(false)
		lifebarFlag2 = true
	end
	if characterData.conditionListSelf:GetTierByID(layerBuffID) > 0 then
		local t = (tempvalue + characterData.conditionListSelf:GetTierByID(layerBuffID)) / 1000
		if isPlayingEndingAnim or isGameEnd then
			if endingAnimTimer > endingSlowFadeinDuration + endingSlowDuration  then
				t = 1
			else
				t = 0.8
			end
		end
		if t<0 then
			t = 0
		end
		if t>1 then
			t = 1
		end
		
		if not startFlag then
			timer = 0
		end
		if t ~= 0.5 then
			startFlag = true
		end
		t = Mathf.Lerp(lastValue,t,timer)
		
		if lastValue ~= t then
			lastValue = t
			timer = 0
		end
		backGroundFloor:SetFloat("_FadePoint",t)
		backGroundWall:SetFloat("_FadePoint",t)
		local coef = t - 0.5
		effectWall.transform.localPosition = CS.UnityEngine.Vector3(effectWallPos[1] + coef * baseRate *effectWallMoveCoef,effectWallPos[2],effectWallPos[3])
		effectFloor.transform.localPosition = CS.UnityEngine.Vector3(effectFloorPos[1]+ coef * baseRate *effectFloorMoveCoef,effectFloorPos[2],effectFloorPos[3])
		--print(t..' '..effectWall.transform.localPosition.x," ",effectFloor.transform.localPosition.x)
		if isPlayingEndingAnim or isGameEnd then
			
		else
			if enemyTransform.localPosition.x < characterMaxPosX then
				
				local charaX = characterStartingPos.x + coef * baseRate * effectWallMoveCoef
				if charaX < characterMinPosX then
					charaX  = characterMinPosX
				end
				characterTransform.localPosition = CS.UnityEngine.Vector3(charaX,characterStartingPos.y,characterStartingPos.z)
			end 
			
			if characterTransform.localPosition.x > characterMinPosX then
				local enemyX = enemyStartingPos.x + coef * baseRate * effectWallMoveCoef
				if enemyX > characterMaxPosX then
					enemyX  = characterMaxPosX
				end
				enemyTransform.localPosition = CS.UnityEngine.Vector3(enemyX,enemyStartingPos.y,enemyStartingPos.z) 
			end
		end
		
	end
	if (not showDialogue) and characterData.conditionListSelf:GetTierByID(layerBuffID) >= endingBuffTier then
		showDialogue = true
		CS.BattleLuaUtility.CharacterDataPlaySkill(11981401,characterData)

		return
		--isPlayingEndingAnim = true
		--print("ending")
	end
	if showDialogue and (not waitAVG) then
		if CS.AVGController.inst ~= nil then
			waitAVG = true
		end
	end
	if  ((waitAVG and CS.UnityEngine.Time.timeScale ~= 0) or ((characterData.conditionListSelf:GetTierByID(layerBuffID) >= endingBuffTier) and(not playAVG()))) and (not isPlayingEndingAnim) then
		isPlayingEndingAnim = true
		return
	end
	if isPlayingEndingAnim then
		--print("endingAnimTimer "..endingAnimTimer.." scale"..CS.UnityEngine.Time.timeScale)
		endingAnimTimer = endingAnimTimer + CS.UnityEngine.Time.unscaledDeltaTime
		if endingAnimTimer <= endingSlowFadeinDuration then
			CS.UnityEngine.Time.timeScale = Mathf.Lerp(1,endingSlowScale,endingAnimTimer / endingSlowFadeinDuration)
		end
		if endingAnimTimer > endingSlowFadeinDuration and  endingAnimTimer > endingSlowFadeinDuration + endingSlowDuration then
			CS.UnityEngine.Time.timeScale = endingSlowScale
		end
		if endingAnimTimer > endingSlowFadeinDuration + endingSlowDuration and  endingAnimTimer <= endingSlowFadeinDuration + endingSlowDuration + endingSlowFadeoutDuration then
			local t1 = endingAnimTimer - (endingSlowFadeinDuration + endingSlowDuration)
			local t2 = t1 / endingSlowFadeoutDuration
			local t3 = Mathf.Lerp(endingSlowScale,1,t2)
			--print(t1..' '..t2..' '..t3)
			CS.UnityEngine.Time.timeScale = t3
		end
		if endingAnimTimer > endingSlowFadeinDuration + endingSlowDuration + endingSlowFadeoutDuration then
			CS.UnityEngine.Time.timeScale = 1
			--isPlayingEndingAnim = false
			enemyTransform.localPosition = CS.UnityEngine.Vector3(enemyTransform.localPosition.x + endingPushRate ,enemyStartingPos.y,enemyStartingPos.z) 
		end
		if not isActionPlayed and endingAnimTimer >= endingSlowFadeinDuration + endingSlowDuration + endingSlowFadeoutDuration - endingActionTime then
			character:SetMemberAnimation("s2", 1)
			isActionPlayed = true
		end
		if endingAnimTimer > endingSlowFinishDuration  then
			isPlayingEndingAnim = false
			EndGame()
		end
	end
end
playAVG = function ()
	return CS.ConfigData.playReplay or CS.GameData.missionAction == null or CS.GameData.missionAction.mission == null or CS.GameData.missionAction.mission.medal1 == false
end
EndGame = function()
	isGameEnd = true
	for i=0,BattleController.enemyTeamHolder.listCharacter.Count-1 do
		local DamageInfo = CS.GF.Battle.BattleDamageInfo()
		BattleController.enemyTeamHolder.listCharacter[i]:UpdateLife(DamageInfo, -999999)
	end
	CS.UnityEngine.Object.Destroy(self.gameObject)
end
--depose
OnDestroy =function()
	PlaySFX("stop")
	--CS.BattleFrameManager.DeRegister(UpdateJoyStick)
	character = nil
	mCurSkill ={}
	xlua.hotfix(CS.GF.Battle.BattleManager,'CheckBaseLine',nil)
	xlua.hotfix(CS.BattleManualSkillController,'OnPointerDown',nil)
	xlua.hotfix(CS.BattleManualSkillController,'OnPointerUp',nil)
	xlua.hotfix(CS.GF.Battle.BattleFriendlyCharacterManager,'Init',nil)
	xlua.hotfix(CS.BattleInteractionController,'DisableRangeLine',nil)
	xlua.hotfix(CS.GF.Battle.BattleFairyController,'SetFairyData',nil)

end
GetTimeFormat = function(value)
	local value2 = math.floor((value - math.floor(value)) * 10)
	local t = string.format("<size=90>%02d</size>:%01d",math.floor(value),value2)
	return t
end
local loss = math.pi /  16
GetInputValue = function(eulerAngle)
	if eulerAngle >= math.pi - loss and eulerAngle < math.pi + loss then
		return math.pi
	end
	if eulerAngle >= math.pi + math.pi/2 - loss and eulerAngle < math.pi + math.pi/2 + loss then
		return math.pi + math.pi/2
	end
	
	if eulerAngle >= math.pi * 2 -loss or (eulerAngle < 0 + loss)  then
		return math.pi * 2
	end
	return eulerAngle
end

HandleJoyStickMove = function(input)
	
	local XPara = speedXPara
	local x =
	CS.Mathf.Clamp(
		character.transform.localPosition.x - math.sin(GetInputValue(input.eulerAngle)) * character.realtimeSpeed * XPara * 1,
		minX,
		maxX
	)
	local y =
	CS.Mathf.Clamp(
		character.transform.localPosition.z + math.cos(GetInputValue(input.eulerAngle)) * character.realtimeSpeed * speedYPara * 1,
		minY,
		maxY
	)
	--print(math.sin(input.eulerAngle))
	--print(math.cos(input.eulerAngle))
	--print("原始速度:"..character.realtimeSpeed .." ".."最终速度:"..character.gun.speed * XPara * input.value)
	
	local offset = CS.UnityEngine.Vector3(x, 0, y)
	if y == character.transform.localPosition.y then
		if isMoving then
			isMoving = false
			--print("wait4")
			character:SetMemberAnimation("wait", 1);
			--moveSoundFrameTimer = 4
		end
	else 
		if isMoving == false then
			isMoving = true
			--print("move")
			character:SetMemberAnimation("move", 1);
		end
		--moveSoundFrameTimer = moveSoundFrameTimer + 1
		--if moveSoundFrameTimer >= 30 * moveSoundInterval then
		--	moveSoundFrameTimer = 0
		--	CS.CommonAudioController.PlayBattle("21Summer_Player_Move")
		--end
	end
	character.transform.localPosition = offset
	--if friendlyArea ~= nil then
	--	local startpos = friendlyArea.localPosition.x
	--	local movedistance = x
	--	if movedistance < 0  then  
	--		movedistance = 0 
	--	end
	--	local finalPos = startpos + movedistance
	--	friendlyArea.localPosition = CS.UnityEngine.Vector3(finalPos,friendlyArea.localPosition.y,friendlyArea.localPosition.z)
	--end
end

CanSkillActive = function(skill)
	if character == nil or character:IsDead() or character:IsWithDraw() then
		return false
	end
	if skill.cdFrame > 0 then
		return false
	end
	if not SkillUtils.GetManaulSkill(character.gun) == nil then
		return false
	end
	if skillActiveTimes >= maxSkillActiveTimes then
		return false
	end
	return true
end
ManualActiveSkill = function(skill)
	if CanSkillActive(skill) then
		SkillUtils.AddManaulSkill(character.gun,skill)
		CS.BattleRecorderController.Instance:AddManualSkill(character.gun)
		skillActiveTimes = skillActiveTimes + 1
		UpdateSkillActiveTimeUI(skillActiveTimes)
		animTimer = -animDelay - 0.1
		--UpdateSkillUI(skill)
		isMoving = false
		BtnShimmer.transform:Find("Img_Shine").gameObject:SetActive(false)
		BtnShimmer.transform:Find("Img_Shine").gameObject:SetActive(true)
	end
end
UpdateSkillActiveTimeUI = function(num)
	local str = "Light"
	if num == 1 then
		DOLightAnim(str..1)
		DOLightAnim(str..2)
		
	end
	if num == 2 then
		DOLightAnim(str..3)
		DOLightAnim(str..4)
	end
	if num == 3 then
		DOLightAnim(str..7)
		DOLightAnim(str..8)
	end
	if num == 4 then
		DOLightAnim(str..11)
		DOLightAnim(str..12)
	end
	if num == 5 then
		DOLightAnim(str..9)
		DOLightAnim(str..10)
	end
	if num == 6 then
		DOLightAnim(str..13)
		DOLightAnim(str..14)
	end
	if num == 7 then
		DOLightAnim(str..5)
		DOLightAnim(str..6)
	end
	
	
end
DOLightAnim = function(name)
	local image = GoLight.transform:Find(name).gameObject:GetComponent(typeof(CS.ExImage))
	local seq = CS.DG.Tweening.DOTween.Sequence()
	seq:Append(image:DOFade(0.5,0.5))
	seq:Append(image:DOFade(0.05,0.3))
end

local resetFlag = false


GetVisionFar = function()
	if animTimer >= animDuration then
		return visionFarBase
	else
		if animTimer <= 0 then
			if animTimer <= -animDelay then
				return visionFarBase + (0.1-(-animTimer -animDelay)) * 30
			else
				return 9999
			end
		else
			return visionFarBase + (animDuration - animTimer) * visionLingerConf
		end
	end
end
local enterFarDuration = 0
local enterNearDuration = 0
local TreeList = {}

function GenColor(r,g,b,a)
	if(r<=1 and g<=1 and b<=1 and a<=1) then	
		return CS.UnityEngine.Color(r,g,b,a)
	else
		return CS.UnityEngine.Color(r/255,g/255,b/255,a/255)
	end
end
IsTargetCreation = function(name)
	return name == '21summerminigame1-1' or name == '21summerminigame1-2' or
	name == '21summerminigame2-1' or name == '21summerminigame2-2' or
	name == '21summerminigame3-1' or name == '21summerminigame3-2'
	
end
GetCreationList = function()
	local sceneGo = BattleController.transform:Find("BattleField/21summerminigame1(Clone)")
	if sceneGo ~= nil then
		for i = 0, sceneGo:GetChildCount()-1 do
			if IsTargetCreation(sceneGo:GetChild(i).gameObject.name) then
				TreeList[#TreeList + 1] = sceneGo:GetChild(i).gameObject:GetComponent(typeof(CS.UnityEngine.SpriteRenderer))
				
				TreeList[#TreeList].color = GenColor(1,1,1,0)
				TreeList[#TreeList].sortingOrder = 3
			end
			
		end
	end
	local creationList = CS.GF.Battle.EffectManager.Instance.mListOrderEffect
	for i=0,creationList.Count-1 do
		
	end
end
local treeFadeRate = 0.1
local treeDisNear = 1.5
local GetTreeDis = function()
	
	return GetVisionFar() - 0.5
end
local GetTreeMaxAlpha = function(distance)
	return 1
end
UpdateCreationState = function()
	local sceneGo = BattleController.transform:Find("BattleField/21summerminigame1(Clone)")
	if sceneGo == nil then
		return
	end
	if #TreeList == 0 then
		GetCreationList()
	end
	for i=1, #TreeList do
		local posSelf = character.listMember[0].transform.position
		local posEnemy = TreeList[i].gameObject.transform.position
		local distance = (posEnemy.x - posSelf.x)*(posEnemy.x - posSelf.x) + visionVerticalConf * visionVerticalConf * (posEnemy.z - posSelf.z)* (posEnemy.z - posSelf.z)
		if distance > GetTreeDis() * GetTreeDis() then
			local t = TreeList[i].color.a
			t = t - treeFadeRate
			if(t < 0) then t = 0 end
			TreeList[i].color = GenColor(1,1,1,t)
			
		else
			local t = TreeList[i].color.a
			t = t + treeFadeRate
			if(t > GetTreeMaxAlpha(distance)) then t = GetTreeMaxAlpha(distance) end
			TreeList[i].color = GenColor(1,1,1,t)
		end
	end
end
function PlaySFX(FXname)
	if FXname == "button" then
		CS.CommonAudioController.PlayBattle("Scar_Button Click")
	end
	if FXname == "loop" then
		CS.CommonAudioController.PlayBattle("Scar_Energy Wave Loop")
	end
	if FXname == "stop" then
		CS.CommonAudioController.PlayBattle("Stop_Battle_loop")
	end
end

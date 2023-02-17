local util = require 'xlua.util'
local config = require ('collaboration/ZLSR/MinigameWorkConfig')
xlua.private_accessible(CS.CommonAudioController)
xlua.private_accessible(CS.CommonController)
xlua.private_accessible(CS.ResManager)
xlua.private_accessible(CS.BattleManualSkillController)
xlua.private_accessible(CS.BattleMemberController)
xlua.private_accessible(CS.BattleFieldTeamHolder)
xlua.private_accessible(CS.BattleUILifeBarController)
xlua.private_accessible(CS.GF.Battle.BattleStatistics)
xlua.private_accessible(CS.GF.Battle.EffectManager)
xlua.private_accessible(CS.GF.Battle.BattleConditionList)
xlua.private_accessible(CS.GF.Battle.CharacterCondition)
xlua.private_accessible(CS.GF.Battle.gsEffect)

local character
local characterData
local playerFeverValue = -1
local feverGuageMax
local totalTimer = 0
local totalFailNum = 0
local isUIPausing = false
local haloObj
local isShown = false
local currentMovingSpd = 0
local characterBuffEffect

local _imgTime1,_imgTime2,_imgTime3,_imgTime4,_imgFeverGauge,spriteListResultScore
local imgGrade,spriteListGrade
local txtFever,txtScore
local spriteListTime
local BattleController
local spine
local dir = 1

local playerScore = 0
local totalBrickNum = 0
local lastFrameHoldingBrickNum = 0
local currentHoldingBrickNum = 0
local stunBuffNum = 0

local stunTimer =0 
local stunAnimFirstFrame = 45
local stunAnimSecondFrame = 45
local isMoving = false
local isStun = false
local lifebarFlag = false
local lastEnergyCount
local currentEnergyCount
local isFever = false
local feverTimer = 0
Awake = function()
	
	math.randomseed(tostring(os.time()):reverse():sub(1, 7))
	config:InitData()
	local RefreshFriendlyTargetList = function(self)
		self.listFriendlyTarget:Clear()
		for i=0,self.enemyTeamHolder.listCharacter.Count -1 do
			local target = self.enemyTeamHolder.listCharacter[i]
			if not target.isPhased then
				self.listFriendlyTarget:Add(target)
			end
		end
		if self.listFriendlyTarget.Count == 0 then
			self:CheckFormation()
		end
	end	
	local DisableRangeLine = function(self)
		return true
	end
	local CheckBaseLine = function(self)
		if (self:CheckAllIsPhased(self.enemyTeamHolder.listCharacter)) then
			self:TriggerBattleFinishEvent()
			return
		end
		if (self:CheckAllIsPhased(self.friendlyTeamHolder.listCharacter)) then
			self:TriggerBattleFinishEvent()
			return
		end
	end
	local OnEffectGenAoeBuffSuccess = function(self)
		--print(currentHoldingBrickNum)
		if isFever and self.mEffectCfg.id == 10449 then
			return
		end
		if currentHoldingBrickNum == 5 and self.mEffectCfg.id ~= 10449 then
			return
		end
		self:OnEffectGenAoeBuffSuccess()
	end
	util.hotfix_ex(CS.GF.Battle.BattleController,'RefreshFriendlyTargetList',RefreshFriendlyTargetList)
	util.hotfix_ex(CS.GF.Battle.BattleController,'CheckBaseLine',CheckBaseLine)
	util.hotfix_ex(CS.BattleInteractionController,'DisableRangeLine',DisableRangeLine)
	util.hotfix_ex(CS.GF.Battle.gsEffect,'OnEffectGenAoeBuffSuccess',OnEffectGenAoeBuffSuccess)
end
Start = function()
	
	
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
	
	BattleController.transform:Find("Canvas/UI/SafeUIRect/DPSSwitch").gameObject:SetActive(false)
	BattleController.transform:Find("Canvas/DynamicCanvas/DPS").gameObject:SetActive(false)
	BattleController.transform:Find("Canvas/UI/Top/Top_Time").gameObject:SetActive(false)
	BattleController.transform:Find("Canvas/UI/PausePanel").gameObject:SetActive(false)
	BattleController.transform:Find("Canvas/DynamicCanvas/TimerText").gameObject:SetActive(false)
	BattleController.transform:Find("Canvas/DynamicCanvas/ManualPanel").gameObject:SetActive(false)
	self.transform:SetParent(CS.BattleUIController.Instance.transform:Find('UI'),false)
	if character == nil then
		character = CS.BattleLuaUtility.GetCharacterByCode(spineCode)
		character.gameObject.transform.localScale = CS.UnityEngine.Vector3(1.2,1.2,1)
		characterData = CS.BattleLuaUtility.GetDataByCode(spineCode)
	end
	spriteListResultScore = goResultScoreItem:GetComponent(typeof(CS.UGUISpriteHolder))
	feverGuageMax = energyMax
	totalTimer = totalTime
	_imgTime1 = imgTimeNum1:GetComponent(typeof(CS.ExImage))
	_imgTime2 = imgTimeNum2:GetComponent(typeof(CS.ExImage))
	_imgTime3 = imgTimeNum3:GetComponent(typeof(CS.ExImage))
	_imgTime4 = imgTimeNum4:GetComponent(typeof(CS.ExImage))
	_imgFeverGauge = feverGuage:GetComponent(typeof(CS.ExImage))
	
	txtFever = feverNum:GetComponent(typeof(CS.ExText))
	txtScore = scoreNum:GetComponent(typeof(CS.ExText))
	spriteListTime = holderTimeNum:GetComponent(typeof(CS.UGUISpriteHolder))
	JoyStrick:GetComponent(typeof(CS.Joystick)).JoystickMoveHandle = JoyStickMove
	JoyStrick:GetComponent(typeof(CS.Joystick)).JoystickEndHandle = JoyStickEnd
	JoyStrick:GetComponent(typeof(CS.Joystick)).JoystickBeginHandle = JoyStickBegin
	UpdateFever(0)
	UpdateScore()
	brickNum:GetComponent(typeof(CS.ExText)).text = totalBrickNum
	goShow.transform:Find("Img_BlurBG").gameObject:AddComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			EndGame()
		end)
	btnPause:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			PauseGame(true)
		end)
	btnExit:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			ExitGame()
		end)
	btnContinue:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			PauseGame(false)
		end)
	btnPutDown:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			DiscardBrick()
		end)
	--CS.BattleScaler.InitScalerByMaxNum(0)
	spine = character.listMember[0]
	imgGrade = goShow.transform:Find("Img_Grade").gameObject:GetComponent(typeof(CS.ExImage))
	spriteListGrade = imgGrade.gameObject:GetComponent(typeof(CS.UGUISpriteHolder))
	CS.BattleFrameManager.Register(
		function() 
			MainLoop()
		end)
end
JoyStickMove = function(input)
	local XPara = speedXPara
	if input.value <= 0.01 then
		return
	end
	if isStun then
		return
	end	
	--print(input.value)
	local x =
	CS.Mathf.Clamp(
		character.transform.localPosition.x - math.sin(input.eulerAngle) * character.realtimeSpeed * XPara * input.value,
		minX,
		maxX
	)
	local y =
	CS.Mathf.Clamp(
		character.transform.localPosition.z + math.cos(input.eulerAngle) * character.realtimeSpeed * speedYPara * input.value,
		minY,
		maxY
	)
	if input.eulerAngle < math.pi then
		if dir >0 then
			dir = -1
			spine:SetDirection(-1)
		end		
		
	else
		if dir <0 then
			dir = 1
			spine:SetDirection(1)
		end
	end
	
	
	--print("原始速度:"..character.realtimeSpeed .." ".."最终速度:"..character.gun.speed * XPara * input.value)
	local offset = CS.UnityEngine.Vector3(x, 0, y)
	character.transform.localPosition = offset
end

JoyStickBegin = function(input)
	
	isMoving  = true
	if not isStun then
		spine:SetSpine(GetMoveCode(),dir)
		
	end	
end

JoyStickEnd = function(input)
	
	--print("End")
	isMoving  = false
	if not isStun then
		spine:SetSpine(GetWaitCode(),dir)
	end	
	
end
OnDestroy = function()
	xlua.hotfix(CS.BattleInteractionController,'DisableRangeLine',nil)
	xlua.hotfix(CS.GF.Battle.BattleController,'RefreshFriendlyTargetList',nil)
	xlua.hotfix(CS.GF.Battle.BattleController,'CheckBaseLine',nil)
	xlua.hotfix(CS.GF.Battle.gsEffect,'OnEffectGenAoeBuffSuccess',nil)
end
Update = function()
	if haloObj ~= nil and haloObj.activeSelf then
		haloObj:SetActive(false)
	end
	
	--MainLoop()
	
end
function MainLoop()
	
	UpdateRemainTime()
	if not lifebarFlag and character.lifeBar ~= nil then
		character.lifeBar.gameObject:SetActive(false)
		lifebarFlag = true
		spine:SetSpine("spwait0",1)
	end
	lastFrameHoldingBrickNum = currentHoldingBrickNum
	lastEnergyCount = currentEnergyCount
	if not isStun then
		UpdateBuff()
		--判断是否fever
		if not isFever then
			UpdateFever(math.ceil(currentEnergyCount * energyBuffCoef))
			CheckFever()
		end
		if playerFeverValue >= feverGuageMax then
			
		end
		--判断是否摔倒
		if stunBuffNum ~= 0 then
			DoStun()
		end
		if isFever then
			
			feverTimer = feverTimer + 0.033333
			if feverTimer >= energyDuration then
				isFever = false
				character.conditionListSelf:RemoveNum(stunBuffIDLeft,999)
				character.conditionListSelf:RemoveNum(stunBuffIDRight,999)
				
				character.conditionListSelf:RemoveNum(energyBuffID,999)
				currentEnergyCount = 0
				UpdateFever(0)
			end
		end
		if lastFrameHoldingBrickNum ~= currentHoldingBrickNum then
			if isMoving then
				spine:SetSpine(GetMoveCode(),dir)
			else
				spine:SetSpine(GetWaitCode(),dir)
			end
			if lastFrameHoldingBrickNum > currentHoldingBrickNum then
				--记录得分
				local addBrickNum = (lastFrameHoldingBrickNum - currentHoldingBrickNum)
				if addBrickNum > 5 then
					addBrickNum = 5
				end
				UpdateBrickScore(totalBrickNum,addBrickNum)
				totalBrickNum = totalBrickNum + addBrickNum
				
				playerScore = playerScore + (addBrickNum * brickScore) +extraBrickScore[addBrickNum]
				
				
				UpdateScoreAnim()
				
			end
		end
	else -- 
		stunTimer = stunTimer + 1
		if stunTimer == stunAnimFirstFrame then
			spine:SetSpine("up", dir)
		end
		if stunTimer >= stunAnimFirstFrame + stunAnimSecondFrame then
			StunFinish()
		end
		stunTimer = stunTimer + 1
		if stunTimer == stunAnimFirstFrame then
			spine:SetSpine("up", dir)
		end
		if stunTimer >= stunAnimFirstFrame + stunAnimSecondFrame then
			StunFinish()
		end
	end
	if math.floor(totalTimer) <= 0 then
		ShowResult()
	end
end
function UpdateBuff()
	currentHoldingBrickNum = character.conditionListSelf:GetTierByID(brickBuffID)
	if currentHoldingBrickNum > lastFrameHoldingBrickNum then
		PlaySFX("pickBrick")
	end
	
	stunBuffNum = character.conditionListSelf:GetTierByID(stunBuffIDLeft)
	if stunBuffNum == 0 then
		stunBuffNum = -character.conditionListSelf:GetTierByID(stunBuffIDRight)	
	end	
	
	currentEnergyCount = character.conditionListSelf:GetTierByID(energyBuffID)
	if currentEnergyCount  > lastEnergyCount then
		if characterBuffEffect == nil then
			characterBuffEffect = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Effect/Buff_ss_zt"),character:GetFirstMember().gameObject.transform,false)
		else
			characterBuffEffect:SetActive(false)
			characterBuffEffect:SetActive(true)
		end
	end
end
function GetMoveCode()
	
	local lastSpd = currentMovingSpd
	if currentHoldingBrickNum > 3 then
		currentMovingSpd = 2
	else
		currentMovingSpd = 1
	end
	if lastSpd ~= currentMovingSpd then
		if currentMovingSpd ==  2 then
			--PlaySFX("stopcook")
			PlaySFX("moveSlow")
		else
			--PlaySFX("stopcook")
			PlaySFX("moveQuick")
		end
		
	end
	if currentHoldingBrickNum == 0 then
		return "move"
	end
	if currentHoldingBrickNum == 1 then
		return "spmove1"
	end
	if currentHoldingBrickNum == 2 then
		return "spmove2"
	end
	if currentHoldingBrickNum == 3 then
		return "spmove3"
	end
	if currentHoldingBrickNum == 4 then
		return "spmove4"
	end
	if currentHoldingBrickNum == 5 then
		return "spmove5"
	end
	return""
end
function GetStunCode()
	PlaySFX("stopcook")
	currentMovingSpd = 0
	if currentHoldingBrickNum == 1 then
		return "Down1"
	end
	if currentHoldingBrickNum == 2 then
		return "Down2"
	end
	if currentHoldingBrickNum == 3 then
		return "Down3"
	end
	if currentHoldingBrickNum == 4 then
		return "Down4"
	end
	if currentHoldingBrickNum == 5 then
		return "Down5"
	end
	return"Down0"
end
function GetWaitCode()
	PlaySFX("stopcook")
	currentMovingSpd = 0
	if currentHoldingBrickNum == 0 then
		return "spwait0"
	end
	if currentHoldingBrickNum == 1 then
		return "spwait1"
	end
	if currentHoldingBrickNum == 2 then
		return "spwait2"
	end
	if currentHoldingBrickNum == 3 then
		return "spwait3"
	end
	if currentHoldingBrickNum == 4 then
		return "spwait4"
	end
	if currentHoldingBrickNum == 5 then
		return "spwait5"
	end
	return""
end
function DoStun()
	--播放倒地动作
	if isFever then
		return
	end
	if stunBuffNum < 0 then
		dir = 1		
	else
		dir = -1
	end
	spine:SetSpine(GetStunCode(), dir)--从右边来车往左边倒，反过来也是
	isStun = true
	isMoving = false
	stunTimer = 0
	PlaySFX("truckHit")
	totalFailNum = totalFailNum +1
end
function StunFinish()
	--清掉砖块和眩晕的标记buff
	DiscardBrick()
	character.conditionListSelf:RemoveNum(stunBuffIDLeft,1)
	character.conditionListSelf:RemoveNum(stunBuffIDRight,1)
	
	if isMoving then
		spine:SetSpine(GetMoveCode(),dir)
	else
		spine:SetSpine(GetWaitCode(),dir)
	end
	isStun = false
end
function UpdateFever(feverCount)
	if playerFeverValue == feverCount then
		return
	end
	if feverCount >0 and feverCount > playerFeverValue then
		PlaySFX("pickPower") 
	end
	playerFeverValue = feverCount
	if playerFeverValue > feverGuageMax then
		playerFeverValue = feverGuageMax
	end
	if playerFeverValue < 0 then
		playerFeverValue = 0
	end
	local feverpercent = playerFeverValue / feverGuageMax
	_imgFeverGauge:DOFillAmount(feverpercent,0.3) 
	txtFever.text = string.format("%d",math.ceil(playerFeverValue)) ..'/'..feverGuageMax
	
end

function PauseGame(isPause)
	isUIPausing = isPause
	if isUIPausing then
		goPause:SetActive(true)
		CS.UnityEngine.Time.timeScale = 0
	else
		goPause:SetActive(false)
		CS.UnityEngine.Time.timeScale = 1
	end
end
function DiscardBrick()
	character.conditionListSelf:RemoveNum(brickBuffID,5)
	lastFrameHoldingBrickNum = 0
	currentHoldingBrickNum = 0
	if isMoving then
		spine:SetSpine(GetMoveCode(),dir)
	else
		spine:SetSpine(GetWaitCode(),dir)
	end
end
function ExitGame()
	CS.UnityEngine.Time.timeScale = 1
	CS.BattleFrameManager.ResumeTime()
	CS.GF.Battle.BattleController.Instance:TriggerBattleFinishEvent(true)
	CS.UnityEngine.Object.Destroy(self.gameObject)
end

function ShowResult()
	if isShown then return end
	isShown = true
	goResultScoreItem:SetActive(false)
	goShow:SetActive(true)
	local curGrade = 1
	for i=1,4 do
		if playerScore >= scoreRankingWork[i] then
			curGrade = i
		end
	end
	imgGrade.sprite = spriteListGrade.listSprite[curGrade-1]
	if CS.GameData.userInfo ~= nil then
		textResultName:GetComponent(typeof(CS.ExText)).text = CS.GameData.userInfo.name
		textResultID:GetComponent(typeof(CS.ExText)).text = CS.GameData.userInfo.userId
	end
	textResultCombo:GetComponent(typeof(CS.ExText)).text = totalBrickNum
	textResultTime:GetComponent(typeof(CS.ExText)).text = totalFailNum
	local strScore = tostring(playerScore) 
	for i=1,string.len(strScore) do
		local num = tonumber(string.sub(strScore,i,i)) 
		local scoreitem =CS.UnityEngine.Object.Instantiate(goResultScoreItem) 
		scoreitem.transform:SetParent(goResultScoreItem.transform.parent,false)
		scoreitem:SetActive(true)
		scoreitem:GetComponent(typeof(CS.ExImage)).sprite = spriteListResultScore.listSprite[num]
	end
	CS.BattleFrameManager.StopTime(true,9999999)
end
function EndGame()
	local ScoreRank = scoreRankingWork[4]
	if playerScore >= ScoreRank then
		
		for i=CS.GF.Battle.BattleController.Instance.enemyTeamHolder.listCharacter.Count-1,0,-1 do
			local DamageInfo = CS.GF.Battle.BattleDamageInfo()
			CS.GF.Battle.BattleController.Instance.enemyTeamHolder.listCharacter[i]:UpdateLife(DamageInfo, -999999)
		end
	else
		CS.GF.Battle.BattleController.Instance:RequestBattleFinish(true)
	end
	CS.BattleFrameManager.ResumeTime()
	CS.UnityEngine.Object.Destroy(goShow)
	CS.UnityEngine.Object.Destroy(self.gameObject)
end
function UpdateRemainTime()
	totalTimer = totalTime - CS.BattleFrameManager.Instance:GetCurBattleTime()
	local timeValue = math.floor(totalTimer)
	if timeValue <0 then
		timeValue = 0
	end
	local minute = math.floor(timeValue / 60)
	local second = timeValue - minute * 60
	if totalTime >= 60 then
		local minute1 = math.floor(minute / 10)
		local minute2 = minute - minute1 * 10
		_imgTime1.sprite = spriteListTime.listSprite[minute1]
		_imgTime2.sprite = spriteListTime.listSprite[minute2]
		
	end
	local sec1 = math.floor(second / 10)
	local sec2 = second - sec1 * 10
	_imgTime3.sprite = spriteListTime.listSprite[sec1]
	_imgTime4.sprite = spriteListTime.listSprite[sec2]
end
function UpdateBrickScore(total,adding)
	self:StopAllCoroutines()
	self:StartCoroutine(CoroutineUpdateBrickScore(total,adding))
end
function CoroutineUpdateBrickScore(total,adding)
	return util.cs_generator(function ()
			for i = 1,adding do
				brickNum:GetComponent(typeof(CS.ExText)).text = total + i
				local scoreEffect = CS.UnityEngine.Object.Instantiate(goScoreEffect,goScoreEffect.transform.parent)
				scoreEffect:SetActive(true)
				coroutine.yield(CS.UnityEngine.WaitForSeconds(0.1))
			end
			brickNum:GetComponent(typeof(CS.ExText)).text = totalBrickNum
		end)
	
end
function UpdateScore()
	txtScore.text = string.format("%05d",playerScore) 
end
function UpdateScoreAnim()
	txtScore:DOText(string.format("%05d",playerScore)  ,0.5,true,CS.DG.Tweening.ScrambleMode.Numerals)
end
function CheckFever()
	if not isFever and playerFeverValue >= feverGuageMax then
		isFever = true
		PlaySFX("enterFever")
		feverTimer = 0
		--CS.CommonAudioController.Instance.bgmSource:Pause(true)
		
		--goFeverEffect:SetActive(true)
		--goFeverEffect2:SetActive(true)
		--goFeverHint:SetActive(true)
		_imgFeverGauge:DOFillAmount(0,energyDuration-0.05):SetEase(CS.DG.Tweening.Ease.Linear)
		--print("Start "..CS.BattleFrameManager.Instance:GetCurBattleTime())
		CS.GF.Battle.SkillUtils.GenBuffViaSkillConfig(characterData,11952601)
	end
end
function PlaySFX(FXname)
	--print(FXname)
	if FXname == "right_click" then
		CS.CommonAudioController.PlayBattle("Click_Correct")
	end
	if FXname == "wrong_click" then
		CS.CommonAudioController.PlayBattle("Click_Incorrect")
	end
	if FXname == "fever_click" then
		CS.CommonAudioController.PlayBattle("Click_Fever")
	end
	if FXname == "music_click" then
		CS.CommonAudioController.PlayBattle("Click_MusicGame")
	end
	if FXname == "enterFever" then
		CS.CommonAudioController.PlayBattle("UI_Fever")
	end
	if FXname == "moveSlow" then
		CS.CommonAudioController.PlayBattle("FS_Slow_Loop")
	end
	if FXname == "moveQuick" then
		CS.CommonAudioController.PlayBattle("FS_Fast_Loop")
	end
	if FXname == "pickBrick" then
		CS.CommonAudioController.PlayBattle("UI_PickBrick")
	end
	if FXname == "truckHit" then
		CS.CommonAudioController.PlayBattle("UI_TruckHit")
	end
	if FXname == "pickPower" then
		CS.CommonAudioController.PlayBattle("UI_PickPower")
	end
	if FXname == "stopcook" then
		CS.CommonAudioController.PlayBattle("Stop_Battle_loop")
	end
	
end
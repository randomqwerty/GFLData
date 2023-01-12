local util = require 'xlua.util'
local config = require ('collaboration/ZLSR/MinigameMusicConfig')
xlua.private_accessible(CS.CommonAudioController)
xlua.private_accessible(CS.CommonController)
xlua.private_accessible(CS.ResManager)
xlua.private_accessible(CS.BattleManualSkillController)
xlua.private_accessible(CS.BattleMemberController)
xlua.private_accessible(CS.GF.Battle.BattleCharacterController)
xlua.private_accessible(CS.GF.Battle.CSkillInstance)
xlua.private_accessible(CS.BattleFieldTeamHolder)
xlua.private_accessible(CS.GF.Battle.BattleStatistics)
xlua.private_accessible(CS.BattleSkillCfg)
xlua.private_accessible(CS.ExButton)
local barLength = 836

local leaderSpine
local txtScore,txtFever
local spriteListResultScore,spriteListTime
local _imgTime1,_imgTime2,_imgTime3,_imgTime4
local _imgFeverGauge,_imgWarningBG
local elementBestAreaWidth,elementBestAreaCenter
local resetFlag = false
local _sliderMusic
local btnMusic
local isHoldingButton = false

local isUIPausing = false
local playerFeverValue = -1
local playerScore = 0
local currentTimer = 0
local currentCursorPos
local currentZonePos
local currentZoneWidth

local lastCursorPos
local lastZonePos
local lastZoneWidth

local nextCursorPos
local nextZonePos
local nextZoneWidth

local EasingFunction

local currentTimeGap
local currentDictPos = 1
local currentFrame = 0

local isFever = false
local lastTimeCenterValue = 0
local lastTimeWidthValue = 0
local outAreaFlag = false
local outAreaTimer = 0

local bestMaintain = 0

local currentMaintain = 0
local feverTimer = 0

local currentAscendSpeed = 0
local currentDescendSpeed = 0
local totalTimer = 0
local isAscend = false
local isDescend = false
local descendTimer = 0
Awake = function()
	
	math.randomseed(tostring(os.time()):reverse():sub(1, 7))
	config:InitData()

end
Start = function()
	local randomMember = math.random(1,7)

	self.transform:SetParent(CS.BattleUIController.Instance.transform:Find('UI'),false)
	--初始化spine
	leaderSpine = CS.UnityEngine.Object.Instantiate(CS.CommonController.GetSpinePrefab(spineCodeList[randomMember]))
	leaderSpine.transform.localScale = CS.UnityEngine.Vector3(160,160,160)
	leaderSpine.transform:SetParent(goSpineHolder.transform,false)
	leaderSpine.transform.localPosition = CS.UnityEngine.Vector3(0,-240,0)
	leaderSpine:SetActive(true)
	leaderSpine:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, "sing", true)
	leaderSpine:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = 15
	--spine:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = 13
	_imgTime1 = Time1:GetComponent(typeof(CS.ExImage))
	_imgTime2 = Time2:GetComponent(typeof(CS.ExImage))
	_imgTime3 = Time3:GetComponent(typeof(CS.ExImage))
	_imgTime4 = Time4:GetComponent(typeof(CS.ExImage))
	spriteListTime = holderTimeNum:GetComponent(typeof(CS.UGUISpriteHolder))
	
	--初始化UI

	_imgFeverGauge = imgFeverBar:GetComponent(typeof(CS.ExImage))
    _imgWarningBG = goWarningBG:GetComponent(typeof(CS.ExImage))
	spriteListResultScore = goResultScoreItem:GetComponent(typeof(CS.UGUISpriteHolder))
	txtScore = textScore:GetComponent(typeof(CS.ExText))
	txtFever = textFever:GetComponent(typeof(CS.ExText))
	_sliderMusic = sliderMusic:GetComponent(typeof(CS.UnityEngine.UI.Slider))
	elementBestAreaWidth = bestAreaMusicValue:GetComponent(typeof(CS.UnityEngine.UI.LayoutElement))
	elementBestAreaCenter = bestAreaLeftValue:GetComponent(typeof(CS.UnityEngine.UI.LayoutElement))
	btnMusic = btnHold:GetComponent(typeof(CS.ExButton))
	btnMusic.onClick:AddListener(
		function()
			OnFeverClickButton()
		end)

	btnMusic:SetButtonPointerDownUpAction(
		function(isUp,pos)
			goMusicButtonPressed:SetActive(not isUp)
			goMusicButtonUnpressed:SetActive(isUp)
			isHoldingButton = not isUp
			if isHoldingButton then
				descendTimer = 0
				isDescend = false
				currentAscendSpeed = cursorAscendStartingSpd
			else
				currentDescendSpeed = cursorDescendStartingSpd
			end
			isAscend = isHoldingButton
		end
	)
	
	goShow.transform:Find("Img_BlurBG").gameObject:AddComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			EndGame()
		end)
	btnPause:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			PauseGame(true)
		end)
	btnPauseQuit:AddComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			ExitGame()
		end)
	btnPauseContinue:AddComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			PauseGame(false)
		end)
	--pdateCombo(0)
	UpdateFever(0)
	UpdateScore(playerScore)
	CS.BattleFrameManager.StopTime(true,9999999)
	CS.BattleUIController.Instance.transform:Find('DynamicCanvas').gameObject:SetActive(false)
	SetCursorPosition(cursorStartingPos)
	SetZonePosition(GetPosValue(startingRangePos,1),GetPosValue(startingRangeWidth,1))
	--StartRound()
	imgAvatar:GetComponent(typeof(CS.ExImage)).sprite = imgAvatar:GetComponent(typeof(CS.UGUISpriteHolder)).listSprite[randomMember-1]
	textAvatarName:GetComponent(typeof(CS.ExText)).text = GetName(nameList[randomMember]) 
	totalTimer = totalTime
end

OnDestroy = function()
	
	
end
Update = function()
	MainLoop()
	
end
function MainLoop()

	if not isFever then
		currentFrame = currentFrame +CS.UnityEngine.Time.deltaTime
		HandleCursorMove()
		CheckScore()
		MoveZone()
		CheckFever()
		currentAscendSpeed = currentAscendSpeed + cursorAscendAcc * CS.UnityEngine.Time.deltaTime
		if currentAscendSpeed > cursorAscendCoef then
			currentAscendSpeed = cursorAscendCoef
		end
		currentDescendSpeed = currentDescendSpeed + cursorDescendAcc * CS.UnityEngine.Time.deltaTime
		if currentDescendSpeed > cursorDescendCoef then
			currentDescendSpeed = cursorDescendCoef
		end
	else
		CountFeverTime()
	end
	if totalTimer > 0 then
		totalTimer = totalTimer - CS.UnityEngine.Time.deltaTime
	end
	UpdateRemainTime()
	if totalTimer <= 0 and not goShow.activeSelf then
		ShowResult()
		return
	end
	if not isHoldingButton and not isDescend  then
		descendTimer  = descendTimer + 1
		if descendTimer >= 0 then
			
			isDescend = true
			descendTimer = 0
		end
	end
end
function HandleCursorMove()
	if isAscend then
		SetCursorPosition(currentCursorPos + currentAscendSpeed * CS.UnityEngine.Time.deltaTime)
	end
	if isDescend then
		SetCursorPosition(currentCursorPos - currentDescendSpeed * CS.UnityEngine.Time.deltaTime)
	end
end
function CheckScore()
	--检查浮标是否在范围内
	local upperLimit = currentZonePos + currentZoneWidth / 2 
	local lowerLimit = currentZonePos - currentZoneWidth / 2 
	if upperLimit > 1 then
		upperLimit = 1
	end
	if lowerLimit < 0 then
		lowerLimit = 0
	end
	--print(currentCursorPos.." "..lowerLimit.." "..upperLimit.." "..currentZonePos.." "..currentZoneWidth)
	if currentCursorPos >= lowerLimit  and currentCursorPos <= upperLimit then
		playerScore = playerScore + baseScore 
		UpdateScore(playerScore)
		UpdateFever(playerFeverValue + fevergain)
		outAreaFlag = false
		
		outAreaTimer = 0
		currentMaintain = currentMaintain + CS.UnityEngine.Time.deltaTime
		if bestMaintain < currentMaintain then
			bestMaintain = currentMaintain
		end
		if not resetFlag then
			resetFlag = true
			goWarningEffect:SetActive(false)
			_imgWarningBG:DOColor(CS.UnityEngine.Color(1,1,1,1),0.1)
			--goCorrect:SetActive(false)
			goCorrect:SetActive(true)
		end
	else
		resetFlag = false
		goCorrect:SetActive(false)
		if 	not outAreaFlag then
			if outAreaTimer >= loseScoreLingerTime then
				outAreaFlag = true
				if playerScore > 0 then
					goWarningEffect:SetActive(true)
				end
			end
			outAreaTimer = outAreaTimer + CS.UnityEngine.Time.deltaTime
			_imgWarningBG.color = CS.UnityEngine.Color(1,1,1,1-(outAreaTimer/loseScoreLingerTime))
		end		
		if outAreaFlag then
			playerScore = playerScore - loseScore
			if playerScore<0 then
				playerScore = 0 
			end
			UpdateScore(playerScore)
			UpdateFever(playerFeverValue - feverlose)
			currentMaintain = 0
		end
	end
end
function MoveZone()

	
	if #dictRangeInfo >= currentDictPos and currentDictPos >= 1 and  currentFrame > dictRangeInfo[currentDictPos].time then
		currentDictPos =currentDictPos + 1		
		SetMoveZoneParameter()
	end
	if currentDictPos == 0 then
		currentDictPos = 1
		SetMoveZoneParameter()
	end
	currentTimer = currentTimer + CS.UnityEngine.Time.deltaTime
	if lastZonePos ~= nextZonePos then
		if currentTimeGap <= 0 then
			currentZonePos = nextZonePos
		else
			if EasingFunction~= nil then	
				currentZonePos = EasingFunction(lastZonePos,nextZonePos, currentTimer / currentTimeGap) --currentZonePos + (nextZonePos-lastZonePos)/currentTimeGap * CS.UnityEngine.Time.deltaTime
			else
				currentZonePos = CS.Mathf.Lerp(lastZonePos,nextZonePos, currentTimer / currentTimeGap)
			end
		end

	end
	if lastZoneWidth  ~= nextZoneWidth  then
		if currentTimeGap <= 0 then
			currentZoneWidth = nextZoneWidth
		else
			if EasingFunction~= nil then	
				currentZoneWidth = EasingFunction(lastZoneWidth,nextZoneWidth, currentTimer / currentTimeGap)-- currentZoneWidth + (nextZoneWidth-lastZoneWidth)/currentTimeGap * CS.UnityEngine.Time.deltaTime
			else
				currentZoneWidth = CS.Mathf.Lerp(lastZoneWidth,nextZoneWidth, currentTimer / currentTimeGap)
			end
			
		end
	end
	SetZonePosition(currentZonePos,currentZoneWidth)
end
function CheckFever()
	if playerFeverValue >= feverGuageMax then
		isFever = true
		
		feverTimer = 0
		_imgFeverGauge:DOFillAmount(0,feverDuration) 
		goFeverEffect:SetActive(true)
		goFeverEffect2:SetActive(true)
		goFeverHint:SetActive(true)
	end
end
function CountFeverTime()
	if isFever then
		feverTimer = feverTimer + CS.UnityEngine.Time.deltaTime
		if feverTimer >= feverDuration then
			isFever = false
			goFeverEffect:SetActive(false)
			goFeverEffect2:SetActive(false)
			goFeverHint:SetActive(false)
			UpdateFever(0)
		end
	end
end
function SetMoveZoneParameter()
	if #dictRangeInfo >= currentDictPos then
		lastZonePos = currentZonePos
		lastZoneWidth = currentZoneWidth
		currentTimer = 0
		nextZonePos = GetPosValue(dictRangeInfo[currentDictPos].pos) 
		nextZoneWidth = GetPosValue(dictRangeInfo[currentDictPos].width) 
		EasingFunction = CS.GF.Battle.SkillUtils.GetEasingFunction(dictRangeInfo[currentDictPos].easeType)
		currentTimeGap = dictRangeInfo[currentDictPos].time - currentFrame
	else
		currentTimeGap = -1
	end
end
--开始轮次
function GetPosValue(parameter,type)
	local value = 0
	if #parameter == 1 then
		value = parameter[1] 
	end
	if #parameter == 2 then
		value = math.random(parameter[1]*1000,parameter[2]*1000)/1000
	end
	
	if value >= 0 then
		RecordValue(value,type)
		return value
	else
		return GetRecordValue(type)
	end	

end
function RecordValue(value,type)
	if type == 1 then
		lastTimeCenterValue = value
	else
		lastTimeWidthValue = value
	end
end
function GetRecordValue(type)
	if type == 1 then
		return lastTimeCenterValue
	else
		return lastTimeWidthValue
	end
end
function SetCursorPosition(pos)
	currentCursorPos = pos
	if currentCursorPos > 1 then
		currentCursorPos = 1
	end
	if currentCursorPos < 0 then
		currentCursorPos = 0
	end
	_sliderMusic.value = currentCursorPos
end
function SetZonePosition(pos,width)
	currentZonePos = pos
	currentZoneWidth = width
	elementBestAreaCenter.preferredWidth = (pos-width/2) * barLength 
	elementBestAreaWidth.minWidth = width* barLength 
end
function UpdateFever(feverCount)
	if playerFeverValue == feverCount then
		return
	end
	playerFeverValue = feverCount
	if playerFeverValue > feverGuageMax then
		playerFeverValue = feverGuageMax
	end
	if playerFeverValue < 0 then
		playerFeverValue = 0
	end
	local feverpercent = playerFeverValue / feverGuageMax
	_imgFeverGauge:DOFillAmount(feverpercent,0.01) 
	txtFever.text = string.format("%d",math.ceil(playerFeverValue)) ..'/'..feverGuageMax
end
function UpdateScore()
	txtScore.text = string.format("%05d",playerScore) 
end
function UpdateScoreAnim()
	txtScore:DOText(string.format("%05d",playerScore)  ,0.5,true,CS.DG.Tweening.ScrambleMode.Numerals)
end
function UpdatePlayerActTime()
	txtPlayerTime.text = string.format("%02d",math.ceil(playerActMaxTime - playerActTimer)) 
end
function PauseGame(isPause)
	isUIPausing = isPause
	if isUIPausing then
		goPauseMenu:SetActive(true)
		CS.UnityEngine.Time.timeScale = 0
	else
		goPauseMenu:SetActive(false)
		CS.UnityEngine.Time.timeScale = 1
	end
end
function OnFeverClickButton()
	if isFever then
		playerScore = playerScore + feverScore
		UpdateScore(playerScore)

	end
end
function ExitGame()
	CS.UnityEngine.Time.timeScale = 1
	CS.BattleFrameManager.ResumeTime()
	CS.GF.Battle.BattleController.Instance:TriggerBattleFinishEvent(true)
	CS.UnityEngine.Object.Destroy(self.gameObject)
end

function ShowResult()
	goResultScoreItem:SetActive(false)
	goShow:SetActive(true)
	if CS.GameData.userInfo ~= nil then
		textResultName:GetComponent(typeof(CS.ExText)).text = CS.GameData.userInfo.name
		textResultID:GetComponent(typeof(CS.ExText)).text = CS.GameData.userInfo.userId
	end
	textResultCombo:GetComponent(typeof(CS.ExText)).text = math.floor(bestMaintain)
	textResultTime:GetComponent(typeof(CS.ExText)).text = totalTime
	local strScore = tostring(playerScore) 
	for i=1,string.len(strScore) do
		local num = tonumber(string.sub(strScore,i,i)) 
		local scoreitem =CS.UnityEngine.Object.Instantiate(goResultScoreItem) 
		scoreitem.transform:SetParent(transResultScore.transform,false)
		scoreitem:SetActive(true)
		scoreitem:GetComponent(typeof(CS.ExImage)).sprite = spriteListResultScore.listSprite[num]
	end
end
function EndGame()
	
	local ScoreRank = scoreRanking[4]
	if playerScore >= ScoreRank then
		
		for i=CS.GF.Battle.BattleController.Instance.enemyTeamHolder.listCharacter.Count-1,0,-1 do
			local DamageInfo = CS.GF.Battle.BattleDamageInfo()
			CS.GF.Battle.BattleController.Instance.enemyTeamHolder.listCharacter[i]:UpdateLife(DamageInfo, -999999)
		end
	else
		CS.GF.Battle.BattleController.Instance:RequestBattleFinish(true)
	end
	CS.BattleFrameManager.ResumeTime()
	CS.UnityEngine.Object.Destroy(GoResult)
	CS.UnityEngine.Object.Destroy(self.gameObject)
end
function UpdateRemainTime()
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
function GetName(NameID)
	return CS.Data.GetLang((NameID))
end
local util = require 'xlua.util'
local config = require ('collaboration/ZLSR/MinigameDanceConfig')
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

local leaderSpine
local centerSpine
local spineList={}

local _imgCombo,_imgComboNum1,_imgComboNum2,_imgComboNum3
local _imgComboCoef,_imgComboCoefNum1,_imgComboCoefNum2,_imgComboCoefDot
local _imgDanceProgressBar,_imgFeverGauge
local _imgTime1,_imgTime2,_imgTime3,_imgTime4
local spriteListCombo,spriteListComboNum,spriteListComboCoef,spriteListComboCoefText,spriteListComboCoefDot,spriteListActionItem,spriteListResultScore,spriteListTime
local txtTime,txtScore,txtFever,txtPlayerTime
local imgGrade,spriteListGrade

local goActionButton1,goActionButton2,goActionButton3,goActionButton4,goActionButton5
local btnActionButton1,btnActionButton2,btnActionButton3,btnActionButton4,btnActionButton5
--local imgAction1,imgAction2,imgAction3,imgAction4,imgAction5
local goActionButton1HL,goActionButton2HL,goActionButton3HL,goActionButton4HL,goActionButton5HL
local playerCombo = 0
local playerMaxCombo = -1
local curComboLevel = 1
local playerFeverValue = 0
local playerScore = 0
local playerUsedTime = 0

local normalRoundCount = 0
local feverValueLimit

local danceSeq = {}
local danceRandomMax,danceRandomMin
local danceRandomMaxExtra = 0
local danceRandomMinExtra = 0

--模式计时器
local isLeadDance = false
local leadDanceTimer = 0
local leadDanceMaxTime

local isPlayerAct = false
local isPlayerActDance = false
local playerActTimer = 0
local playerActMaxTime
local curPlayerActPosition = 1
local playerActSuccessCount = 0
local isPlayerActSuccessFinish = false

local WaitForPlayerDance1 = false
local WaitForPlayerDance2 = false
local isPlayerDance = false
local playerDanceTimer  =0
local playerDanceMaxTime  =0
--local roundRandomDanceCodeIndex
local danceTotalFrame

local isUIPausing = false
local danceActionItemList = {}
local randomDanceList = {}
local roundDanceCount = 1
local roundDanceFrame = 0

local isFever = false
local isFeverStandby  = false --前置准备
local isFeverExit  = false --退出fever

local feverTimer = 0
local playerDanceCoroutine
local battleController
local startingWait = true
local startingTimer = 0
local playerDanceDelayTimer = 0
local thisRoundDanced = false
local thisRoundWaited = false
local feverClickTime = 0

local totalTimer = 0
Awake = function()
	
	math.randomseed(tostring(os.time()):reverse():sub(1, 7))
	config:InitData()
	feverValueLimit = feverGuageMax
	danceRandomMin = startingRandomRangeMin
	danceRandomMax = startingRandomRangeMax
end
Start = function()
	self.transform:SetParent(CS.BattleUIController.Instance.transform:Find('UI'),false)
	--初始化spine
	leaderSpine = CS.UnityEngine.Object.Instantiate(CS.CommonController.GetSpinePrefab(leaderSpineCode))
	leaderSpine.transform.localScale = CS.UnityEngine.Vector3(160,160,160)
	leaderSpine.transform:SetParent(GetSpineHolder(-1),false)
	leaderSpine.transform.localPosition = CS.UnityEngine.Vector3(0,-240,0)
	leaderSpine:SetActive(true)
	leaderSpine:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, "dance_wait", true)
	leaderSpine:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = 14
	playerDanceMaxTime = playerDanceExtraWaitFrame / 30
	--spine:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = 13
	totalTimer  = totalTime
	for i=1,7 do
		local spine = CS.UnityEngine.Object.Instantiate(CS.CommonController.GetSpinePrefab(dancerSpineCode[i]))
		spine.transform.localScale = CS.UnityEngine.Vector3(160,160,160)
		spine.transform:SetParent(GetSpineHolder(i),false)
		spine.transform.localPosition = CS.UnityEngine.Vector3(0,-160,0)
		spine:SetActive(true)
		
		spine:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, "dance_wait", true)
		spine:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = 15
		if i == 4 then
			centerSpine = spine
		end
		spineList[i] = spine
	end
	
	--初始化UI
	_imgCombo = imgCombo:GetComponent(typeof(CS.ExImage))
	_imgComboNum1 = imgComboNum1:GetComponent(typeof(CS.ExImage))
	_imgComboNum2 = imgComboNum2:GetComponent(typeof(CS.ExImage))
	_imgComboNum3 = imgComboNum3:GetComponent(typeof(CS.ExImage))
	_imgComboCoef = imgComboCoefText:GetComponent(typeof(CS.ExImage))
	_imgComboCoefNum1 = imgComboCoef1:GetComponent(typeof(CS.ExImage))
	_imgComboCoefNum2 = imgComboCoef2:GetComponent(typeof(CS.ExImage))
	_imgComboCoefDot = imgComboCoefDot:GetComponent(typeof(CS.ExImage))
	_imgFeverGauge = imgFeverGauge:GetComponent(typeof(CS.ExImage))
	_imgDanceProgressBar = goDanceProgressBar:GetComponent(typeof(CS.ExImage))
	_imgTime1 = Time1:GetComponent(typeof(CS.ExImage))
	_imgTime2 = Time2:GetComponent(typeof(CS.ExImage))
	_imgTime3 = Time3:GetComponent(typeof(CS.ExImage))
	_imgTime4 = Time4:GetComponent(typeof(CS.ExImage))
	imgGrade = goShow.transform:Find("Img_Grade").gameObject:GetComponent(typeof(CS.ExImage))
	spriteListGrade = imgGrade.gameObject:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListCombo = imgCombo:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListComboNum = imgCombo.transform.parent:Find("Num").gameObject:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListComboCoef = imgComboCoefText:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListComboCoefText = imgComboCoef1:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListComboCoefDot = imgComboCoefDot:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListActionItem = goDanceActionItem.transform:Find("Img_ActionIcon"):GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListTime = holderTimeNum:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListResultScore = goResultScoreItem:GetComponent(typeof(CS.UGUISpriteHolder))
	txtPlayerTime = textDanceRemainTime:GetComponent(typeof(CS.ExText))
	txtScore = textScore:GetComponent(typeof(CS.ExText))
	txtFever = textFever:GetComponent(typeof(CS.ExText))
	
	goActionButton1 = GetActionButton(1)
	goActionButton2 = GetActionButton(2)
	goActionButton3 = GetActionButton(3)
	goActionButton4 = GetActionButton(4)
	goActionButton5 = GetActionButton(5)
	btnActionButton1 = goActionButton1:GetComponent(typeof(CS.ExButton))
	btnActionButton2 = goActionButton2:GetComponent(typeof(CS.ExButton))
	btnActionButton3 = goActionButton3:GetComponent(typeof(CS.ExButton))
	btnActionButton4 = goActionButton4:GetComponent(typeof(CS.ExButton))
	btnActionButton5 = goActionButton5:GetComponent(typeof(CS.ExButton))
	goActionButton1HL = goActionButton1.transform:Find("Img_HighLight").gameObject
	goActionButton2HL = goActionButton2.transform:Find("Img_HighLight").gameObject
	goActionButton3HL = goActionButton3.transform:Find("Img_HighLight").gameObject
	goActionButton4HL = goActionButton4.transform:Find("Img_HighLight").gameObject
	goActionButton5HL = goActionButton5.transform:Find("Img_HighLight").gameObject
	
	btnActionButton1.onClick:AddListener(
		function()
			OnPlayerActButtonClick(1)
		end)
	btnActionButton2.onClick:AddListener(
		function()
			OnPlayerActButtonClick(2)
		end)
	btnActionButton3.onClick:AddListener(
		function()
			OnPlayerActButtonClick(3)
		end)
	btnActionButton4.onClick:AddListener(
		function()
			OnPlayerActButtonClick(4)
		end)
	btnActionButton5.onClick:AddListener(
		function()
			OnPlayerActButtonClick(5)
		end)
	btnActionButton1:SetButtonPointerDownUpAction(
		function(isUp,pos)
			if isPlayerAct then
				goActionButton1HL:SetActive(not isUp)
			end
		end
	)
	btnActionButton2:SetButtonPointerDownUpAction(
		function(isUp,pos)
			if isPlayerAct then
				goActionButton2HL:SetActive(not isUp)
			end
		end
	)
	btnActionButton3:SetButtonPointerDownUpAction(
		function(isUp,pos)
			if isPlayerAct then
				goActionButton3HL:SetActive(not isUp)
			end
		end
	)
	btnActionButton4:SetButtonPointerDownUpAction(
		function(isUp,pos)
			if isPlayerAct then
				goActionButton4HL:SetActive(not isUp)
			end
		end
	)
	btnActionButton5:SetButtonPointerDownUpAction(
		function(isUp,pos)
			if isPlayerAct then
				goActionButton5HL:SetActive(not isUp)
			end
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
	btnPauseEndGame:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			ExitGame()
		end)
	btnPauseContinue:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			PauseGame(false)
		end)
	btnFever:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			ClickFeverButton()
		end)
	UpdateCombo(0)
	UpdateFever(0)
	UpdateRemainTime()
	UpdateScore(playerScore)
	CS.BattleFrameManager.StopTime(true,9999999)
	CS.BattleUIController.Instance.transform:Find('DynamicCanvas').gameObject:SetActive(false)
	battleController = CS.GF.Battle.BattleController.Instance
	goDanceDancer.transform.parent.gameObject:AddComponent(typeof(CS.UnityEngine.CanvasGroup))
	--StartRound()
	StartingWait()
end

OnDestroy = function()
	
	
end
Update = function()
	if startingWait then
		startingTimer = startingTimer  + CS.UnityEngine.Time.deltaTime 
		if startingTimer >= preWaitTimeFrameFirstRound / 30 then
			startingWait = false
			
			StartRound()
		else
			SetDanceProgressBar((startingTimer / (preWaitTimeFrameFirstRound / 30) ))
			UpdatePlayerActTimeStarting()
			return
		end	
		
	end
	if isLeadDance or isPlayerAct then
		playerDanceDelayTimer = playerDanceDelayTimer + CS.UnityEngine.Time.deltaTime
		if not thisRoundDanced and  playerDanceDelayTimer >= npcDanceDelay / 30 then
			StartPlayerDance()			
			thisRoundDanced = true
		end
	end
	if isLeadDance  then
		leadDanceTimer = leadDanceTimer + CS.UnityEngine.Time.deltaTime
		
		if leadDanceTimer >= leadDanceMaxTime then
			FinishLeadDance()
		end
	end
	if isPlayerAct then
		playerActTimer = playerActTimer + CS.UnityEngine.Time.deltaTime
		if playerActTimer > playerActMaxTime then
			playerActTimer = playerActMaxTime
		end
		SetDanceProgressBar((playerActTimer / playerActMaxTime))
		UpdatePlayerActTime()
		if playerActTimer >= playerActMaxTime then
			FinishPlayerActPhase(false)
		end
		
	end
	
	if isPlayerDance then
		playerDanceTimer = playerDanceTimer + CS.UnityEngine.Time.deltaTime
		if playerDanceTimer >= 1 and  not thisRoundWaited then
			centerSpine:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, "dance_wait", true)
			thisRoundWaited = true
		end
		if playerDanceTimer >= playerDanceMaxTime then
			FinishPlayerDancePhase()
		end
	end
	if isFeverStandby then
		feverTimer = feverTimer + CS.UnityEngine.Time.deltaTime
		if feverTimer >= feverStartingFrame / 30 then
			StartFever()
		end
	end
	if isFever  then
		feverTimer = feverTimer + CS.UnityEngine.Time.deltaTime
		if feverTimer >= feverDuration then
			ExitFever()
		end
	end
	if isFeverExit  then
		feverTimer = feverTimer + CS.UnityEngine.Time.deltaTime
		if feverTimer >= feverEndingFrame / 30 then
			StartRound()
			isFeverExit  = false
		end
	end
	if totalTimer > 0 then
		totalTimer = totalTimer - CS.UnityEngine.Time.deltaTime
	end
	UpdateRemainTime()
end
function StartingWait()
	goDanceReadyItem:SetActive(true)
end
--开始轮次
function StartRound()
	goDanceReadyItem:SetActive(false)
	if totalTimer <= 0 then
		ShowResult()
		return
	end
	if playerFeverValue >= feverValueLimit then
		StartFeverRound()
	else
		thisRoundWaited = false
		thisRoundDanced = false
		playerDanceDelayTimer = 0 
		StartNormalRound()
	end
end
function StartFeverRound()
	isFeverStandby = true
	feverTimer = 0
	--fever演出 山田播特殊动作 其他人播惊讶
	centerSpine:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, yamadaFeverAnimCode, true)
	leaderSpine:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, "dance_wait", true)
	
	goDanceButtonHolder:GetComponent(typeof(CS.UnityEngine.CanvasGroup)):DOFade(0,0.3)
	goDanceDancer.transform.parent.gameObject:GetComponent(typeof(CS.UnityEngine.CanvasGroup)):DOFade(0,0.3)
	--btnFever:SetActive(true)
	goActionButton1:SetActive(false)
	goActionButton2:SetActive(false)
	goActionButton3:SetActive(false)
	goActionButton4:SetActive(false)
	goActionButton5:SetActive(false)
	PlaySFX("enterFever")
	effectFever:SetActive(false)
	effectFever:SetActive(true)
end
function StartFever()
	
	--goActionButton1:SetActive(false)
	--goActionButton2:SetActive(false)
	--goActionButton3:SetActive(false)
	--goActionButton4:SetActive(false)
	--goActionButton5:SetActive(false)
	for i=1,#spineList do
		if i ~= 4 then
			spineList[i]:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, npcFeverAnimCode, true)
			if i >4 then
				spineList[i].transform.localScale = CS.UnityEngine.Vector3(-160,160,160)
			end
		end	
	end
	isFeverStandby = false
	isFever = true
	feverTimer = 0
	btnFever:SetActive(true)
	btnFever:GetComponent(typeof(CS.UnityEngine.CanvasGroup)):DOFade(1,0.1)
	--播放一个动画使得Fever槽扣除
	_imgFeverGauge:DOFillAmount(0,feverDuration) 
end
function ExitFever()
	isFeverExit = true
	isFever = false
	feverTimer = 0
	btnFever:GetComponent(typeof(CS.UnityEngine.CanvasGroup)):DOFade(0,0.1)
	btnFever:SetActive(false)
	goDanceButtonHolder:GetComponent(typeof(CS.UnityEngine.CanvasGroup)):DOFade(1,0.3)
	goDanceDancer.transform.parent.gameObject:GetComponent(typeof(CS.UnityEngine.CanvasGroup)):DOFade(1,0.3)
	goActionButton1:SetActive(true)
	goActionButton2:SetActive(true)
	goActionButton3:SetActive(true)
	goActionButton4:SetActive(true)
	goActionButton5:SetActive(true)
	UpdateFever(0)
	leaderSpine:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, "dance_wait", true)
	for i=1,#spineList do
		spineList[i]:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, "dance_wait", true)	
	end
	for i=1,#spineList do
		if i >4 then
			spineList[i].transform.localScale = CS.UnityEngine.Vector3(160,160,160)
		end
	end
end
function StartNormalRound()
	normalRoundCount = normalRoundCount + 1
	--产生本轮的舞蹈序列
	GenerateDanceSequence()
	--领舞
	StartLeadDance()
end
function GenerateDanceSequence()
	danceSeq = {}
	--检查并更新随机上下限
	if dictDanceRandRangeChange[normalRoundCount] ~= nil then
		danceRandomMin = dictDanceRandRangeChange[normalRoundCount][1]
		danceRandomMax = dictDanceRandRangeChange[normalRoundCount][2]
	end
	--先检查有没有预组
	if dictDancePreset[normalRoundCount] ~= nil then
		for i=1,#dictDancePreset[normalRoundCount] do
			if dictDancePreset[normalRoundCount][i] >=1 and dictDancePreset[normalRoundCount][i] <=5 then
				danceSeq[i] = dictDancePreset[normalRoundCount][i]
			else
				danceSeq[i] = math.random(1,5)
			end			
		end
	else
		local rdMax = danceRandomMax + danceRandomMaxExtra
		local rdMin = danceRandomMin + danceRandomMinExtra
		if rdMin > rdMax then
			rdMin = rdMax
		end
		local randnum = math.random(rdMin,rdMax)
		for i=1,randnum do
			danceSeq[i] = math.random(1,5)
		end
	end
	--更新舞蹈用时
	danceTotalFrame = 0
	for  i = 1 ,30 do	
		randomDanceList[i] = math.random(1,#actionAnimCode)
	end
	playerActMaxTime = baseWaitTime + extraWaitTime * #danceSeq
	local playerActFrame = playerActMaxTime * 30
	local danceFrameCnt = 0
	for  i = 1 ,30 do	
		danceFrameCnt = danceFrameCnt + danceAnimFrame[randomDanceList[i] ] 
		if danceFrameCnt >= playerActFrame then
			roundDanceCount = i
			roundDanceFrame = danceFrameCnt
			break
		end
	end
	--roundRandomDanceCodeIndex = math.random(1,#actionAnimCode)
	--print(actionAnimCode[roundRandomDanceCodeIndex].. ' '..danceAnimFrame[roundRandomDanceCodeIndex] )
	
end
function DiscardDanceActionItem()
	for i=1,#danceActionItemList do
		danceActionItemList[i]:SetActive(false)
	end
end
function ShowDanceActionItem(pos,type,state)
	local item 
	if #danceActionItemList < pos then
		item = CS.UnityEngine.Object.Instantiate(goDanceActionItem)
		item.transform:SetParent(goDanceActionItem.transform.parent,false)
		danceActionItemList[#danceActionItemList+1] = item
	else
		item = danceActionItemList[pos]
	end
	if item ~= nil then
		item:SetActive(true)
		SetActionItemState(item,type,state)
	end
end
function SetActionItemState(item,type,state)
	if item == nil then
		return
	end
	
	local correctBG = item.transform:Find("Img_CorrectBG")
	local failedBG = item.transform:Find("Img_ErrorBG")
	local correctMark = item.transform:Find("Img_Correct")
	local failedMark = item.transform:Find("Img_Error")
	local actionIcon = item.transform:Find("Img_ActionIcon")
	actionIcon.gameObject:GetComponent(typeof(CS.ExImage)).sprite = spriteListActionItem.listSprite[type-1]
	correctBG.gameObject:SetActive(state > 0)
	correctMark.gameObject:SetActive(state > 0)
	failedBG.gameObject:SetActive(state < 0)
	failedMark.gameObject:SetActive(state < 0)
	if state > 0 then
		PlaySFX("right_click")
	end
	if state < 0 then
		PlaySFX("wrong_click")
	end
end
function SetDanceProgressBar(value)
	_imgDanceProgressBar.fillAmount = value
end
---phase 领舞
function StartLeadDance()
	
	DiscardDanceActionItem()
	SetDanceProgressBar(0)
	--切换到领舞模式
	goDanceLeader:SetActive(false)
	goDanceDancer:SetActive(true)
	--显示actionItem
	
	--开始领舞计时
	isLeadDance = true
	leadDanceTimer = 0
	leadDanceMaxTime = preWaitTimeFrame / 30
	for i=1,#danceSeq do
		ShowDanceActionItem(i,danceSeq[i],0)
	end
	--
	PlayLeadDanceAnim()
end
--

function PlayLeadDanceAnim()
	battleController:StartCoroutine(CoroutineLeadDance())
end
function CoroutineLeadDance()
	return util.cs_generator(function ()
			for i = 1,roundDanceCount do
				leaderSpine:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, actionAnimCode[randomDanceList[i]], false)
				coroutine.yield(CS.UnityEngine.WaitForSeconds(danceAnimFrame[randomDanceList[i]] /30)) 	
			end								
			leaderSpine:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, "dance_wait", true)
		end)
end
function FinishLeadDance()
	isLeadDance = false
	--leaderSpine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, "dance_wait",true, 0)
	
	StartPlayerAction()
end

---phase 玩家操作
function StartPlayerAction()
	
	
	isPlayerAct = true
	--isPlayerActDance = true
	--玩家可操作时间更新
	playerActMaxTime = baseWaitTime + extraWaitTime * #danceSeq
	leadDanceMaxTime = playerActMaxTime
	playerActTimer = 0
	leadDanceTimer = 0
	--顶栏切换
	goDanceLeader:SetActive(false)
	goDanceDancer:SetActive(true)
	--goDanceDancer.transform:GetChild(0).gameObject:SetActive(true)
	--goDanceDancer.transform:GetChild(1).gameObject:SetActive(true)
	SetDanceProgressBar(1)
	UpdatePlayerActTime()
	--set to 1
	curPlayerActPosition = 1
	playerActSuccessCount = 0
	
	
	
end
function StartPlayerDance()
	--舞蹈表演提前到玩家操作开始
	for i=1,#spineList do
		if i ~= 4 then
			--roll一次npc是否成功表演
			local isAccident = (math.random(1,100) <= npcSpecialAnimProp * 100)
			local breakPoint = -1
			if isAccident then
				breakPoint = math.random(1,roundDanceCount)
			end
			PlayNPCDanceAnim(spineList[i],breakPoint)
		else
			playerDanceCoroutine = CoroutinePlayerDance(spineList[i],-1)
			self:StartCoroutine(playerDanceCoroutine)
		end	
	end
end
function OnPlayerActButtonClick(pos)
	if isPlayerAct then
		--检查当前按下的按钮和跳舞队列是否匹配
		if pos == danceSeq[curPlayerActPosition] then
			OnSuccessAct(pos)
		else
			OnFailedAct(pos)
		end
	end
end
--成功选择一个舞步
function OnSuccessAct(pos)
	--combo计数
	UpdateCombo(playerCombo + 1)
	UpdateFever(playerFeverValue + 1)
	--顶部确认
	ShowDanceActionItem(curPlayerActPosition,danceSeq[curPlayerActPosition],1)
	
	curPlayerActPosition = curPlayerActPosition + 1
	playerActSuccessCount = playerActSuccessCount + 1
	
	--如果输入完成最后一个舞步，提前进行结算
	if curPlayerActPosition > #danceSeq then
		FinishPlayerActPhase(true)
	end
end
function OnFailedAct(pos)
	--combo计数
	UpdateCombo(0)
	--顶部确认
	ShowDanceActionItem(curPlayerActPosition,danceSeq[curPlayerActPosition],-1)
	curPlayerActPosition = curPlayerActPosition + 1
	FinishPlayerActPhase(false)
end
function FinishPlayerActPhase(isSuccess)
	isPlayerActSuccessFinish  = isSuccess
	playerUsedTime = playerUsedTime + math.ceil(playerActMaxTime - playerActTimer)
	-- 如果失败则扣完combo
	if not isSuccess then
		UpdateCombo(0)
	end
	-- 结算舞步分数
	playerScore = playerScore + (playerActSuccessCount * baseScore[curComboLevel]) 
	if isSuccess then
		--如果本轮成功，结算额外分数（时间分）
		playerScore = playerScore + math.ceil((playerActMaxTime - playerActTimer) * timeScoreCoef)
		_imgDanceProgressBar:DOFillAmount(1,0.5) 
		--显示perfect特效
		effectPerfect:SetActive(false)
		effectPerfect:SetActive(true)
	else
		SetDanceProgressBar(0)
	end
	isPlayerAct = false	
	UpdateScoreAnim()
	--隐藏顶部的时间显示
	--goDanceDancer.transform:GetChild(0).gameObject:SetActive(false)
	--goDanceDancer.transform:GetChild(1).gameObject:SetActive(false)
	--表演阶段
	--CallPlayerDancePhase(1)
	isPlayerDance = true
	if isPlayerActSuccessFinish then
		
	else
		self:StopAllCoroutines()
		--centerSpine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, "dance_wait", true, 0)
		centerSpine:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, yamadaFailedAnimCode, false)
	end
	
end
---phase 玩家操作表演

function PlayNPCDanceAnim(spine,breakPoint)
	battleController:StartCoroutine(CoroutinePlayerDance(spine,breakPoint))
end
function CoroutinePlayerDance(spine,breakPoint)
	return util.cs_generator(function ()
			local t = 1
			for i = 1,roundDanceCount do
				
				if breakPoint  == i  then
					spine:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, npcSpecialAnimCode, false)
					coroutine.yield(CS.UnityEngine.WaitForSeconds(0.6))
					spine:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, npcSpecialAnimCode, false)
					break
				else
					spine:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, actionAnimCode[randomDanceList[i]], false)
				end
				t = i 
				coroutine.yield(CS.UnityEngine.WaitForSeconds(danceAnimFrame[randomDanceList[i]] /30)) 
				
			end	
			if t == roundDanceCount	then											
				spine:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, "dance_wait", true)
			else
				coroutine.yield(CS.UnityEngine.WaitForSeconds(1)) 
				spine:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, "dance_wait", true)
			end
		end)
end
function FinishPlayerDancePhase()
	--spine归位
	for i=1,#spineList do
		spineList[i]:GetComponent(typeof(CS.SkeletonAnimation)).state:SetAnimation(0, "dance_wait", true)
	end
	battleController:StopAllCoroutines()
	self:StopAllCoroutines()
	isPlayerDance = false
	playerDanceTimer = 0
	--开始下个轮次
	StartRound()
	--ShowResult()
end
function GetSpineHolder(pos)
	local transSpineHolder = goSpineHolder.transform
	
	if pos <= 0 then
		return transSpineHolder:Find("Leader")
	else
		return transSpineHolder:Find("Dancer"..pos)
	end
end
function GetActionButton(pos)
	local transButtonHolder = goDanceButtonHolder.transform
	return transButtonHolder:Find("Button_Action"..pos).gameObject
end

function UpdateCombo(comboNum)
	--print("UpdateCombo"..comboNum)
	playerCombo = comboNum
	if playerMaxCombo < playerCombo then
		playerMaxCombo = playerCombo 
	end
	local combolevel = 1
	local coef = playerComboCoeflv1
	if comboNum >= comboLvRequire[2] then
		combolevel = 2
	end
	if comboNum >= comboLvRequire[3] then
		combolevel = 3
	end
	
	if curComboLevel ~= combolevel then
		curComboLevel = combolevel
		
		if combolevel == 1 then
			--AddBuff(4822)
			--AddCreatorBuff(4822)
			--if comboEffectObj1 ~= nil then
			--	comboEffectObj1:SetActive(true)
			--else
			--	comboEffectObj1 =CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Effect/DXG_combo_fire01"),transComboEffectHolder,false)
			--end
			--else
			--if comboEffectObj1 ~= nil then
			--	comboEffectObj1:SetActive(false)
			--end
		end
		if combolevel == 2 then
			--AddBuff(4823)
			--AddCreatorBuff(4823)
			--if comboEffectObj2 ~= nil then
			--	comboEffectObj2:SetActive(true)
			--else
			--	comboEffectObj2 =CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Effect/DXG_combo_fire02"),transComboEffectHolder,false)
			--end
			--else
			--if comboEffectObj2 ~= nil then
			--	comboEffectObj2:SetActive(false)
			--end
		end
		if combolevel == 3 then
			--AddBuff(4824)
			--AddCreatorBuff(4824)
			--if comboEffectObj3 ~= nil then
			--	comboEffectObj3:SetActive(true)
			--else
			--	comboEffectObj3 =CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Effect/DXG_combo_fire03"),transComboEffectHolder,false)
			--end
			--else
			--if comboEffectObj3 ~= nil then
			--	comboEffectObj3:SetActive(false)
			--end
		end
		
	end
	danceRandomMaxExtra = 0
	danceRandomMinExtra = 0
	for i=1,#dictComboExtraStartingRangeUpCombo do
		
		if playerCombo >= dictComboExtraStartingRangeUpCombo[i] then
			danceRandomMaxExtra = dictComboExtraStartingRangeUpValue[i]
		end
	end
	for i=1,#dictComboExtraStartingRangeDownCombo do
		
		if playerCombo >= dictComboExtraStartingRangeDownCombo[i] then
			danceRandomMinExtra = dictComboExtraStartingRangeDownValue[i]
		end
	end
	
	_imgCombo.sprite = spriteListCombo.listSprite[combolevel-1]
	_imgComboCoef.sprite = spriteListComboCoef.listSprite[combolevel-1]
	_imgComboCoefDot.sprite = spriteListComboCoefDot.listSprite[combolevel-1]
	--判断数字位数和字符
	local comboStr = tostring(comboNum)
	local strcount = string.len(comboStr)
	--print(comboNum..' '..strcount)
	if strcount == 1 then
		_imgComboNum1.sprite = spriteListComboNum.listSprite[(combolevel-1)*10 +comboNum]
		imgComboNum2:SetActive(false)
		imgComboNum3:SetActive(false)
	end
	if strcount == 2 then
		local ten = math.modf(comboNum/10)
		local one = math.modf(comboNum - 10 * ten)
		_imgComboNum2.sprite = spriteListComboNum.listSprite[(combolevel-1)*10 +ten]
		_imgComboNum1.sprite = spriteListComboNum.listSprite[(combolevel-1)*10 +one]
		imgComboNum2:SetActive(true)
		imgComboNum3:SetActive(false)
	end
	if strcount == 3 then
		local hundred = math.modf(comboNum/100)
		local ten = math.modf((comboNum- 100 * hundred)/10)
		local one = math.modf(comboNum - (100 * hundred) - (10 * ten))
		_imgComboNum3.sprite = spriteListComboNum.listSprite[(combolevel-1)*10 +hundred]
		_imgComboNum2.sprite = spriteListComboNum.listSprite[(combolevel-1)*10 +ten]
		_imgComboNum1.sprite = spriteListComboNum.listSprite[(combolevel-1)*10 +one]
		imgComboNum2:SetActive(true)
		imgComboNum3:SetActive(true)
	end
	--倍率系数
	
	local one, minor
	local coef = baseScore[combolevel] / baseScore[1] 
	one, minor = math.modf(coef)
	minor = math.modf(minor * 10)
	_imgComboCoefNum1.sprite = spriteListComboCoefText.listSprite[(combolevel-1)*10 + one]
	_imgComboCoefNum2.sprite = spriteListComboCoefText.listSprite[(combolevel-1)*10 + minor]
end
function UpdateFever(feverCount)
	playerFeverValue = feverCount
	if playerFeverValue > feverValueLimit then
		playerFeverValue = feverValueLimit
	end
	local feverpercent = playerFeverValue / feverValueLimit
	_imgFeverGauge:DOFillAmount(feverpercent,0.1) 
	txtFever.text = playerFeverValue..'/'..feverValueLimit
end
function UpdateScore()
	txtScore.text = string.format("%06d",playerScore) 
end
function UpdateScoreAnim()
	txtScore:DOText(string.format("%06d",playerScore)  ,0.5,true,CS.DG.Tweening.ScrambleMode.Numerals)
end
function UpdatePlayerActTimeStarting()
	--txtPlayerTime.text = string.format("%02d",math.ceil((preWaitTimeFrameFirstRound / 30) - startingTimer)) 
end
function UpdatePlayerActTime()
	--txtPlayerTime.text = string.format("%02d",math.ceil(playerActMaxTime - playerActTimer)) 
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
function ExitGame()
	CS.UnityEngine.Time.timeScale = 1
	CS.BattleFrameManager.ResumeTime()
	battleController:TriggerBattleFinishEvent(true)
	CS.UnityEngine.Object.Destroy(self.gameObject)
end

function ShowResult()
	goResultScoreItem:SetActive(false)
	goShow:SetActive(true)
	local curGrade = 1
	for i=1,4 do
		if playerScore >= scoreRanking[i] then
			curGrade = i
		end
	end
	imgGrade.sprite = spriteListGrade.listSprite[curGrade-1]
	if CS.GameData.userInfo ~= nil then
		textResultName:GetComponent(typeof(CS.ExText)).text = CS.GameData.userInfo.name
		textResultID:GetComponent(typeof(CS.ExText)).text = CS.GameData.userInfo.userId
	end
	textResultCombo:GetComponent(typeof(CS.ExText)).text = playerMaxCombo 
	textResultTime:GetComponent(typeof(CS.ExText)).text = feverClickTime 
	local strScore = tostring(playerScore) 
	for i=1,string.len(strScore) do
		local num = tonumber(string.sub(strScore,i,i)) 
		local scoreitem =CS.UnityEngine.Object.Instantiate(goResultScoreItem) 
		scoreitem.transform:SetParent(goResultScoreItem.transform.parent,false)
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
	CS.UnityEngine.Object.Destroy(goShow)
	CS.UnityEngine.Object.Destroy(self.gameObject)
end
function ClickFeverButton()
	--fever点击得分，加combo
	if CS.UnityEngine.Time.deltaTime > 0 then
		playerScore = playerScore + feverScoreCoef
		UpdateScore()
		UpdateCombo(playerCombo + 1)
		PlaySFX("fever_click")
		feverClickTime = feverClickTime +1
		local feverPerfectEffect = CS.UnityEngine.Object.Instantiate(effectPerfect,effectPerfect.transform.parent)
		feverPerfectEffect:SetActive(true)
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
	
	
end

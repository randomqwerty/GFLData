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
local spriteListCombo,spriteListComboNum,spriteListComboCoef,spriteListComboCoefText,spriteListComboCoefDot,spriteListActionItem,spriteListResultScore
local txtTime,txtScore,txtFever,txtPlayerTime

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

local danceTotalFrame

local isUIPausing = false
local danceActionItemList = {}
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
	leaderSpine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, "wait", true, 0)
	leaderSpine:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = 15
	--spine:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = 13
	
	for i=1,7 do
		local spine = CS.UnityEngine.Object.Instantiate(CS.CommonController.GetSpinePrefab(dancerSpineCode[i]))
		spine.transform.localScale = CS.UnityEngine.Vector3(160,160,160)
		spine.transform:SetParent(GetSpineHolder(i),false)
		spine.transform.localPosition = CS.UnityEngine.Vector3(0,-160,0)
		spine:SetActive(true)
		
		spine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, "wait", true, 0)
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
	spriteListCombo = imgCombo:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListComboNum = imgCombo.transform.parent:Find("Num").gameObject:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListComboCoef = imgComboCoefText:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListComboCoefText = imgComboCoef1:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListComboCoefDot = imgComboCoefDot:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListActionItem = goDanceActionItem.transform:Find("Img_ActionIcon"):GetComponent(typeof(CS.UGUISpriteHolder))
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
	UpdateCombo(0)
	UpdateFever(0)
	UpdateScore(playerScore)
	CS.BattleFrameManager.StopTime(true,9999999)
	CS.BattleUIController.Instance.transform:Find('DynamicCanvas').gameObject:SetActive(false)
	
	StartRound()
end

OnDestroy = function()
	
	
end
Update = function()
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
		SetDanceProgressBar(1-(playerActTimer / playerActMaxTime))
		UpdatePlayerActTime()
		if playerActTimer >= playerActMaxTime then
			FinishPlayerActPhase(false)
		end
		
	end
	if isPlayerActDance then
		leadDanceTimer = leadDanceTimer + CS.UnityEngine.Time.deltaTime
		if leadDanceTimer >= leadDanceMaxTime then
			isPlayerActDance = false
			CallPlayerDancePhase(2)
		end
	end
	if isPlayerDance then
		playerDanceTimer = playerDanceTimer + CS.UnityEngine.Time.deltaTime
		if playerDanceTimer >= playerDanceMaxTime then
			FinishPlayerDancePhase()
		end
	end
end
--开始轮次
function StartRound()
	if playerFeverValue >= feverValueLimit then
		StartFeverRound()
	else
		StartNormalRound()
	end
end
function StartFeverRound()
	
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
		local randnum = math.random(danceRandomMin,danceRandomMax)
		for i=1,randnum do
			danceSeq[i] = math.random(1,5)
		end
	end
	--更新舞蹈用时
	danceTotalFrame = 0
	local printlog = "round"..normalRoundCount.." Seq:"
	for i=1,#danceSeq do
		danceTotalFrame = danceTotalFrame + danceAnimFrame[danceSeq[i]] 
		printlog = printlog..danceSeq[i]..' '
	end
	print(printlog)
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
	if normalRoundCount == 1 then
		leadDanceMaxTime = preWaitTimeFrameFirstRound / 30
	else
		leadDanceMaxTime = preWaitTimeFrame / 30
	end
	for i=1,#danceSeq do
		ShowDanceActionItem(i,danceSeq[i],0)
	end
	--
end
--

function PlayLeadDanceAnim()
	self:StartCoroutine(CoroutineLeadDance())
end
function CoroutineLeadDance()
	return util.cs_generator(function ()
			for i=1,#danceSeq do
				leaderSpine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, actionAnimCode[i], false, 0)
				coroutine.yield(CS.UnityEngine.WaitForSeconds(danceAnimFrame[danceSeq[i]] /30)) 
			end							
			
		end)
end
function FinishLeadDance()
	isLeadDance = false
	--leaderSpine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, "wait",true, 0)
	
	StartPlayerAction()
end

---phase 玩家操作
function StartPlayerAction()
	
	PlayLeadDanceAnim()
	isPlayerAct = true
	isPlayerActDance = true
	--玩家可操作时间更新
	playerActMaxTime = baseWaitTime + extraWaitTime * #danceSeq
	leadDanceMaxTime = ((danceTotalFrame + playerDanceExtraWaitFrame) / 30)
	playerActTimer = 0
	leadDanceTimer = 0
	--顶栏切换
	goDanceLeader:SetActive(false)
	goDanceDancer:SetActive(true)
	goDanceDancer.transform:GetChild(0).gameObject:SetActive(true)
	goDanceDancer.transform:GetChild(1).gameObject:SetActive(true)
	SetDanceProgressBar(1)
	UpdatePlayerActTime()
	--set to 1
	curPlayerActPosition = 1
	playerActSuccessCount = 0
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
		_imgDanceProgressBar:DOFillAmount(0,0.5) 
	else
		SetDanceProgressBar(0)
	end
	isPlayerAct = false	
	UpdateScoreAnim()
	--隐藏顶部的时间显示
	goDanceDancer.transform:GetChild(0).gameObject:SetActive(false)
	goDanceDancer.transform:GetChild(1).gameObject:SetActive(false)
	--表演阶段
	CallPlayerDancePhase(1)
end
---phase 玩家操作表演
function CallPlayerDancePhase(pos)
	--这个阶段的表演如果比领舞完成的更早，就要等待；领舞等待时间结束才进行
	if pos == 1 then
		WaitForPlayerDance1 = true
	else
		WaitForPlayerDance2 = true
	end
	if WaitForPlayerDance1 and WaitForPlayerDance2 then
		WaitForPlayerDance1 = false
		WaitForPlayerDance2 = false
		StartPlayerDancePhase()
	end
	
end
function StartPlayerDancePhase()
	isPlayerDance = true
	playerDanceTimer = 0
	playerDanceMaxTime = ((danceTotalFrame + playerDanceExtraWaitFrame) / 30)
	--主角演出：若玩家成功则播放舞蹈序列，否则播失败动画
	if isPlayerActSuccessFinish then
		PlayNPCDanceAnim(centerSpine,-1)
	else
		centerSpine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, yamadaFailedAnimCode, true, 0)
	end
	--其余npc演出
	
	for i=1,#spineList do
		if i ~= 4 then
			--roll一次npc是否成功表演
			local isAccident = (math.random(1,100) <= npcSpecialAnimProp * 100)
			local breakPoint = -1
			if isAccident then
				breakPoint = math.random(1,5)
			end
			PlayNPCDanceAnim(spineList[i],breakPoint)
		end	
	end
end
function PlayNPCDanceAnim(spine,breakPoint)
	self:StartCoroutine(CoroutinePlayerDance(spine,breakPoint))
end
function CoroutinePlayerDance(spine,breakPoint)
	return util.cs_generator(function ()
			for i=1,#danceSeq do
				if breakPoint >0 and breakPoint == i then
					spine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, npcSpecialAnimCode, true, 0)
					break
				end
				spine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, actionAnimCode[i], false, 0)
				coroutine.yield(CS.UnityEngine.WaitForSeconds(danceAnimFrame[danceSeq[i]] /30)) 
			end							
			
		end)
end
function FinishPlayerDancePhase()
	--spine归位
	for i=1,#spineList do
		spineList[i]:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, "wait", true, 0)
	end
	isPlayerDance = false
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
	
	_imgCombo.sprite = spriteListCombo.listSprite[combolevel-1]
	_imgComboCoef.sprite = spriteListComboCoef.listSprite[combolevel-1]
	_imgComboCoefDot.sprite = spriteListComboCoefDot.listSprite[combolevel-1]
	--判断数字位数和字符
	local comboStr = tostring(comboNum)
	local strcount = string.len(comboStr)
	print(comboNum..' '..strcount)
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
	textResultCombo:GetComponent(typeof(CS.ExText)).text = playerMaxCombo 
	textResultTime:GetComponent(typeof(CS.ExText)).text = playerUsedTime
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
	
	for i=CS.GF.Battle.BattleController.Instance.enemyTeamHolder.listCharacter.Count-1,0,-1 do
		local DamageInfo = CS.GF.Battle.BattleDamageInfo()
		CS.GF.Battle.BattleController.Instance.enemyTeamHolder.listCharacter[i]:UpdateLife(DamageInfo, -999999)
	end
	CS.BattleFrameManager.ResumeTime()
	CS.UnityEngine.Object.Destroy(GoResult)
	CS.UnityEngine.Object.Destroy(self.gameObject)
end

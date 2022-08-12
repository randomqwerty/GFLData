local util = require 'xlua.util'
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

SkillActive = function(active,showCD)
	
end

local config = require ('Battle/2022EventMiniGameConfig')
local LuaPointerUpFlag = false
local LuaPointerDownFlag = false
local LuaPointerDownSkillId = 0
local charactercode = "summer_commander"
local characterGridPosX = 0
local characterGridPosY = 1
local maxGrid = 3
local charPos
local characterStatus = 0 -- 0:wait 1:瞬移中 2:进行攻击中
local characterFacetoward = true
local isGameFinish = false
local isResultPageAnimFinish = false

local isDieEvent = false
local isCheckEvent = false

local attack_duration = 0 -- 这个读技能信息
local isPlayingMoveAction = false
local moveTimer = 0 
local moveActionTimer = 0
local attackActionTimer = 0
local buttonUp,buttonDown,buttonLeft,buttonRight
local ImgUp,ImgDown,ImgLeft,ImgRight
local imgCombo,imgComboNum1,imgComboNum2,imgComboNum3
local imgComboCoef,imgComboCoefNum1,imgComboCoefNum2,imgComboCoefDot
local spriteListCombo,spriteListComboNum,spriteListComboCoef,spriteListComboCoefText,spriteListComboCoefDot
local transComboEffectHolder, transFeverEffectHolder
local imgFever,textFeverCount,textScore
local moveVector
local mCurSkill ={}
local SkillUtils = CS.GF.Battle.SkillUtils
local alphaTestThreshold = 0.5

local playerScore = 0
local playerCombo = 0
local playerMaxCombo = 0
local PlayerFeverValue = 0
local isFever = false
local isFeverStarted = false
local feverTimer = 0
local totaltimer = 0

local summonAutoDieBuffID = 4817
local hitBuffID = 4818
local comboBreakBuffID = 4820

local melonBreakCount = {0,0,0,0,0,0,0}
local member
local skillbase
local curComboLevel = 0
local comboEffectObj1
local comboEffectObj2
local comboEffectObj3
local useHold = true
local creatorCharacter

--Awake：初始化数据
Awake = function()
	
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
	local Die = function(self)
		if self:IsSummon() then
			local t,c = self.conditionListSelf:GetTierByID(summonAutoDieBuffID)
			if t == 0 then
				OnSummonDie(self.gun.summonInfo.id,self.gameObject.transform.position)
			else
				OnOutBound(self.gun.summonInfo.id)
			end
		end
		
		
		self:Die()
	end
	local PlaySkill = function(self,skill)
		if skill.info:IsDeathRattle() then
			local t,c = self.character.conditionListSelf:GetTierByID(summonAutoDieBuffID)
			if t ~= 0 and skill.info.skillGroupId == 119469 then
				return
			end
		end
		self:PlaySkill(skill)
	end
	local _HandleMovementtEvent = function(self,pEvent)
		self:_HandleMovementtEvent(pEvent)
		if pEvent.EffectCfg.duration > 0 and self.mMovementCtrl ~= nil then
			if curComboLevel == 2 then
				self.mMovementCtrl.TotalFrame = phase2Speed * pEvent.EffectCfg.duration
			end
			if curComboLevel == 3 then
				self.mMovementCtrl.TotalFrame = phase3Speed * pEvent.EffectCfg.duration
			end
		end
	end
	util.hotfix_ex(CS.GF.Battle.BattleController,'RefreshFriendlyTargetList',RefreshFriendlyTargetList)
	util.hotfix_ex(CS.GF.Battle.CSkillInstance,'_HandleMovementtEvent',_HandleMovementtEvent)
	util.hotfix_ex(CS.GF.Battle.BattleCharacterController,'Die',Die)
	util.hotfix_ex(CS.BattleMemberController,'PlaySkill',PlaySkill)
	--初始化随机数
	math.randomseed(tostring(os.time()):reverse():sub(1, 7))
	
	config:InitData()
	totaltimer = gameTimer * 30
	CS.UICoinBattleTimer.Instance:StopAllCoroutines()
	CS.UICoinBattleTimer.Instance:SetTimer(gameTimer,function ()
			GameFinish()
		end)
end

--Start: 加载组件
Start = function()
	--禁止人物拖动并锁定镜头
	CS.BattleInteractionController.isGuideInteractable = false
	CS.BattleInteractionController.isGuideCanNotScale = false
	CS.BattleInteractionController.isGuideCanNotOffset = false
	CS.GF.Battle.SkillUtils.AutoSkill = false	
	CS.GF.Battle.BattleController.Instance.resetAutoSkill = true
	CS.GF.Battle.BattleController.Instance.resetCameraLock = true
	
	--注册相机
	self.transform:SetParent(CS.BattleUIController.Instance.transform:Find('UI'),false)
	--self:GetComponent('Canvas').worldCamera = CS.UnityEngine.Camera.main
	--注册人物
	if character == nil then
		character = CS.BattleLuaUtility.GetCharacterByCode(charactercode)
	end
	--注册人物技能
	--mCurSkill[0] = character.gun:GetSkillByGroupId(406901)
	-- 人物扶正
	charPos = character.transform
	--charPos.localPosition = CS.UnityEngine.Vector3(charPos.localPosition.x, characterY, charPos.localPosition.z)
	member = character.listMember[0]
	skillbase = CS.GameData.listBTSkillCfg:GetDataById(11940201)
	member.transform.localPosition = CS.UnityEngine.Vector3(playerOffset[1],playerOffset[2],playerOffset[3])
	--character.listMember[0].mesh.sortingOrder = 1
	character:SetMemberAnimation("wait", 1)
	
	--CS.BattleUIManualSkillController.Instance.gameObject:SetActive(false)
	CS.BattleLuaUtility.SwitchUIManualPannel(false) -- 关闭手动技能面板
	
	--InitSkill1(SkillLabel1,mCurSkill[0],3)
	--InitSkill1(SkillLabel2,mCurSkill[1],1)
	--InitSkill1(SkillLabel3,mCurSkill[2],2)
	--InitSkill1(SkillLabel4,mCurSkill[3],4)
	mCurSkill[1] = character.gun:GetSkillByGroupId(119402)
	mCurSkill[2] = character.gun:GetSkillByGroupId(119403)
	mCurSkill[3] = character.gun:GetSkillByGroupId(119404)
	mCurSkill[4] = character.gun:GetSkillByGroupId(119415)
	mCurSkill[5] = character.gun:GetSkillByGroupId(119416)
	mCurSkill[6] = character.gun:GetSkillByGroupId(119417)
	mCurSkill[7] = character.gun:GetSkillByGroupId(119417)
	BattleController = CS.GF.Battle.BattleController.Instance
	buttonUp = BtnUp:GetComponent(typeof(CS.ExButton))
	buttonDown = BtnDown:GetComponent(typeof(CS.ExButton))
	buttonLeft = BtnLeft:GetComponent(typeof(CS.ExButton))
	buttonRight = BtnRight:GetComponent(typeof(CS.ExButton))
	buttonSkill = BtSKill:GetComponent(typeof(CS.ExButton))
	ImgUp = BtnUp:GetComponent(typeof(CS.ExImage))
	ImgDown = BtnDown:GetComponent(typeof(CS.ExImage))
	ImgLeft = BtnLeft:GetComponent(typeof(CS.ExImage))
	ImgRight = BtnRight:GetComponent(typeof(CS.ExImage))
	BattleController.transform:Find("Canvas/UI/SafeUIRect/DPSSwitch").gameObject:SetActive(false)
	BattleController.transform:Find("Canvas/SafeRect/DPS").gameObject:SetActive(false)
	--local cameratrans = BattleController.transform:Find("BattleField/CameraPositionDynamic/CameraPositionStatic")
	--cameratrans.position = CS.UnityEngine.Vector3(-2.35,cameratrans.position.y,cameratrans.position.z)
	buttonSkill = BtSKill:GetComponent(typeof(CS.ExButton))
	ImgUp.alphaHitTestMinimumThreshold = alphaTestThreshold
	ImgDown.alphaHitTestMinimumThreshold = alphaTestThreshold
	ImgLeft.alphaHitTestMinimumThreshold = alphaTestThreshold
	ImgRight.alphaHitTestMinimumThreshold = alphaTestThreshold
	InitButtons()
	spriteListCombo = ImgCombo:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListComboNum = ImgCombo.transform.parent:Find("Num").gameObject:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListComboCoef = ImgComboCoef:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListComboCoefText = ImgComboCoefNum1:GetComponent(typeof(CS.UGUISpriteHolder))
	spriteListComboCoefDot = ImgComboCoefDot:GetComponent(typeof(CS.UGUISpriteHolder))
	imgCombo = ImgCombo:GetComponent(typeof(CS.ExImage))
	imgComboNum1 = ImgComboNum1:GetComponent(typeof(CS.ExImage))
	imgComboNum2 = ImgComboNum2:GetComponent(typeof(CS.ExImage))
	imgComboNum3 = ImgComboNum3:GetComponent(typeof(CS.ExImage))
	imgComboCoef = ImgComboCoef:GetComponent(typeof(CS.ExImage))
	imgComboCoefNum1 = ImgComboCoefNum1:GetComponent(typeof(CS.ExImage))
	imgComboCoefNum2 = ImgComboCoefNum2:GetComponent(typeof(CS.ExImage))
	imgComboCoefDot = ImgComboCoefDot:GetComponent(typeof(CS.ExImage))
	imgFever = ImgFeverBar:GetComponent(typeof(CS.ExImage))
	textFeverCount = TextFeverCount:GetComponent(typeof(CS.ExText))
	textScore = TextScore:GetComponent(typeof(CS.ExText))
	transComboEffectHolder = GoComboEffectHolder.transform
	transFeverEffectHolder = GoFeverEffectHolder.transform
	--print("currentDifficulty"..currentDifficulty)
	UpdateCombo(0)
	UpdateFever(0)
	UpdateScore(playerScore)
	CS.BattleFrameManager.Register(
		function() 
			MainLoop()
		end)
	--GameFinish()
end

local friendlyArea
local friendlyAreaInitalPos

function InitButtons()
	if useHold then
		buttonUp.canHold = true
		buttonDown.canHold = true
		buttonLeft.canHold = true
		buttonRight.canHold = true
	else
		buttonUp.onClick:AddListener(
			function()
				TryMove(1)
			end)
		buttonDown.onClick:AddListener(
			function()
				TryMove(2)
			end)
		buttonLeft.onClick:AddListener(
			function()
				TryMove(3)			
			end)
		buttonRight.onClick:AddListener(
			function()
				TryMove(4)			
			end)
	end
	buttonSkill.onClick:AddListener(
		function()
			PlayAttack()
		end)
	BtnResult:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			if isResultPageAnimFinish then
				EndGame()
			end
		end)
end
function TryMove(dir)
	--当前在wait状态才能够移动
	if characterStatus == 0 then
		--检查移动的方向是否合法
		if dir == 1 and characterGridPosY >= maxGrid  then
			return 
		end
		if dir == 2 and characterGridPosY <= 0 then
			return 
		end
		if dir == 3 and characterGridPosX <= 0 then
			return 
		end
		if dir == 4 and characterGridPosX >= maxGrid then
			return 
		end
		local movespeed = gridDistanceVertical
		if dir == 3 or dir == 4 then
			movespeed = gridDistanceHorizontal
		end
		movespeed = movespeed / move_duration
		if dir == 2 or dir == 3 then
			movespeed = - movespeed
		end
		if dir <= 2 then
			moveVector = CS.UnityEngine.Vector3(0,0,movespeed)
		else
			moveVector = CS.UnityEngine.Vector3(movespeed,0,0)
			
		end
		characterStatus = 1
		isPlayingMoveAction = true
		if not isFever then
			character:SetMemberAnimationSolo("move2", false)
			PlaySFX("Move")
		end
		if dir == 1 then
			characterGridPosY = characterGridPosY + 1
		end
		if dir == 2 then
			characterGridPosY = characterGridPosY - 1
		end
		if dir == 3 then
			characterGridPosX = characterGridPosX - 1
			character:SetFaceToward(false)
			characterFacetoward = false
		end
		if dir == 4 then
			characterGridPosX = characterGridPosX + 1
			character:SetFaceToward(true)
			characterFacetoward = true
		end
	end
end
function PlayAttack()
	
	local rand = math.random(1,3)
	if not characterFacetoward then
		rand = math.random(4,6)
	end
	local skill = mCurSkill[rand]
	if characterStatus == 0 and not isFever and CanSkillActive(skill) then
		isDieEvent = false
		isCheckEvent = false
		SkillUtils.AddManaulSkill(character.gun,skill)
		CS.BattleRecorderController.Instance:AddManualSkill(character.gun)
		characterStatus  = 2
		attack_duration = skill.info._duration
		FinishPlayMoveAction()
		
	end
end
function MainLoop()
	if characterStatus == 1 then
		moveTimer = moveTimer + 1
		charPos.localPosition = charPos.localPosition + moveVector
		if moveTimer >= move_duration then
			characterStatus = 0
			moveTimer = 0
		end
	end
	if characterStatus == 2 then
		attackActionTimer = attackActionTimer + 1
		if attackActionTimer >= attack_duration then
			CheckHitMelon()
			characterStatus = 0
			attackActionTimer = 0
			if not isFever then
				character:SetMemberAnimationSolo("wait")
			end
			if not isCheckEvent and not isDieEvent then
				BreakCombo()
			end
			if isCheckEvent and not isDieEvent then
				PlaySFX("HitNoBreak")
			end
		else
			local dir = 1
			if not characterFacetoward then dir = -1 end
			member:SetDirection(dir)
		end
	end
	if isPlayingMoveAction then
		moveActionTimer = moveActionTimer + 1
		if moveActionTimer >= move_action_duration then
			FinishPlayMoveAction()
			if not isFever then
				character:SetMemberAnimationSolo("wait")
			end
		end
	end
	if isFeverStarted then
		feverTimer = feverTimer + 1 
		imgFever:DOFillAmount((feverDuration-feverTimer)/feverDuration,0.1) 
		if feverTimer >= feverDuration then
			EndFever()
		end
	end
end
Update = function()
	if isGameFinish then
		return
	end
	PlayTest()
	if useHold then
		MoveButtonCheck()
	end
	if characterStatus == 0 and not isFever then
		ImgSkillReady:SetActive(true)
	else
		ImgSkillReady:SetActive(false)
	end
	if character.lifeBar ~= nil then
		character.lifeBar.gameObject:SetActive(false)
	end
	if isFever and not isFeverStarted and CheckFeverBuff() then
		FeverAnim()
	end
	
	
end
function MoveButtonCheck()
	if buttonUp.isDown then
		TryMove(1)
	end
	if buttonDown.isDown then
		TryMove(2)
	end
	if buttonLeft.isDown then
		TryMove(3)
	end
	if buttonRight.isDown then
		TryMove(4)
	end
	
end
function PlayTest()
	if CS.UnityEngine.Input.GetKey(CS.UnityEngine.KeyCode.UpArrow) or CS.UnityEngine.Input.GetKey(CS.UnityEngine.KeyCode.W) then
		TryMove(1)
	end
	if CS.UnityEngine.Input.GetKey(CS.UnityEngine.KeyCode.DownArrow) or CS.UnityEngine.Input.GetKey(CS.UnityEngine.KeyCode.S) then
		TryMove(2)
	end
	if CS.UnityEngine.Input.GetKey(CS.UnityEngine.KeyCode.LeftArrow) or CS.UnityEngine.Input.GetKey(CS.UnityEngine.KeyCode.A) then
		TryMove(3)
	end
	if CS.UnityEngine.Input.GetKey(CS.UnityEngine.KeyCode.RightArrow) or CS.UnityEngine.Input.GetKey(CS.UnityEngine.KeyCode.D) then
		TryMove(4)
	end
	if CS.UnityEngine.Input.GetKey(CS.UnityEngine.KeyCode.Space) or CS.UnityEngine.Input.GetKey(CS.UnityEngine.KeyCode.J) or CS.UnityEngine.Input.GetKey(CS.UnityEngine.KeyCode.K) then
		PlayAttack()
	end
end
function OnOutBound(summonid)
	local melonid = dictMelonPair[summonid]
	if outBoundBreakCombo and melonid ~= 5 then
		BreakCombo()
	end

end
function OnSummonDie(summonid,pos)
	local melonid = dictMelonPair[summonid]
	--计算combo值
	playerCombo = playerCombo + 1
	if isFever and melonid == 5 then
		UpdateCombo(playerCombo)
		PlaySFX("HitNormal")
		return
	end
	if melonid == 4 then -- 炸弹
		ExplodeEffect(2,pos)
		PlaySFX("HitIce")
	end
	if melonid == 5 then -- 炸弹
		BreakCombo()
		ExplodeEffect(1,pos)
		PlaySFX("HitBomb")
	end
	if melonid == 7 then
		PlaySFX("HitHuge")
	end
	if melonid == 1 or melonid == 2 or melonid == 3 or melonid == 6 then
		PlaySFX("HitNormal")
	end
	PlayerFeverValue = PlayerFeverValue + melonFever[melonid]
	if PlayerFeverValue > feverValueLimit then
		PlayerFeverValue = feverValueLimit
	end
	local baseScore = melonScore[melonid]
	local combocoef = playerComboCoeflv1
	local fevercoef = feverCoef1
	UpdateCombo(playerCombo)
	if not isFever then
		UpdateFever(PlayerFeverValue)
	end
	if playerCombo >= combolv2 then
		fevercoef = feverCoef2
		combocoef = playerComboCoeflv2
	end
	if playerCombo >= combolv3 then
		fevercoef = feverCoef3
		combocoef = playerComboCoeflv3
	end
	if not isFeverStarted then
		fevercoef = 1.0
	end
	
	playerScore = playerScore + math.floor(baseScore * combocoef * fevercoef) 
	UpdateScore(playerScore)
	if PlayerFeverValue == feverValueLimit then
		StartFever()
	end
	melonBreakCount[melonid] = melonBreakCount[melonid] + 1
	isDieEvent = true
end 
function CheckHitMelon()
	local friendlyTeamList = BattleController.friendlyTeamHolder.listCharacter
	for i=0, friendlyTeamList.Count-1 do
		local char = friendlyTeamList[i]
		if char:IsSummon() then
			local t,c = char.conditionListSelf:GetTierByID(hitBuffID)
			if t >0 then
				isCheckEvent = true
				playerCombo = playerCombo + 1
				UpdateCombo(playerCombo)
				char.conditionListSelf:RemoveNum(hitBuffID,t)
			end
		end
	end
	
end
function BreakCombo()
	
	playerCombo = 0
	UpdateCombo(0)
end
function ExplodeEffect(type,pos)
	local str = "Effect/XDZY/XDZY_TY2_sp"
	if type == 2 then
		str = "Effect/SM_ice_bao"
	end
	local explodeffect =CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath(str),BattleController.holderCreation,false)
	explodeffect.transform.position = pos
end
function StartFever()
	if not isFever then
		isFever = true
		isFeverStarted = false
		feverTimer = 0
		AddBuff(4825)
		
		
	end
end
function CheckFeverBuff()
	local t,c = character.conditionListSelf:GetTierByID(4825)
	return t <= 0
end
function FeverAnim()
	isFeverStarted = true
	if feverEffectObj == nil then
		feverEffectObj =CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Effect/DXG_sudu_xian"),transFeverEffectHolder,false)
	else
		feverEffectObj:SetActive(true)
	end
end
function EndFever()
	isFever = false
	isFeverStarted = false
	feverTimer = 0
	PlayerFeverValue = 0
	UpdateFever(PlayerFeverValue)
	if feverEffectObj ~= nil then
		feverEffectObj:SetActive(false)
	end
	character:SetMemberAnimationSolo("wait")
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
	return true
end
function FinishPlayMoveAction()
	moveActionTimer = 0
	isPlayingMoveAction = false
end
function UpdateCombo(comboNum)
	playerCombo = comboNum
	if playerMaxCombo < playerCombo then
		playerMaxCombo = playerCombo 
	end
	local combolevel = 1
	local coef = playerComboCoeflv1
	if comboNum >= combolv2 then
		combolevel = 2
		coef = playerComboCoeflv2
	end
	if comboNum >= combolv3 then
		combolevel = 3
		coef = playerComboCoeflv3
	end
	
	if curComboLevel ~= combolevel then
		curComboLevel = combolevel
		
		if combolevel == 1 then
			AddBuff(4822)
			AddCreatorBuff(4822)
			if comboEffectObj1 ~= nil then
				comboEffectObj1:SetActive(true)
			else
				comboEffectObj1 =CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Effect/DXG_combo_fire01"),transComboEffectHolder,false)
			end
		else
			if comboEffectObj1 ~= nil then
				comboEffectObj1:SetActive(false)
			end
		end
		if combolevel == 2 then
			AddBuff(4823)
			AddCreatorBuff(4823)
			if comboEffectObj2 ~= nil then
				comboEffectObj2:SetActive(true)
			else
				comboEffectObj2 =CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Effect/DXG_combo_fire02"),transComboEffectHolder,false)
			end
		else
			if comboEffectObj2 ~= nil then
				comboEffectObj2:SetActive(false)
			end
		end
		if combolevel == 3 then
			AddBuff(4824)
			AddCreatorBuff(4824)
			if comboEffectObj3 ~= nil then
				comboEffectObj3:SetActive(true)
			else
				comboEffectObj3 =CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Effect/DXG_combo_fire03"),transComboEffectHolder,false)
			end
		else
			if comboEffectObj3 ~= nil then
				comboEffectObj3:SetActive(false)
			end
		end
		
	end
	
	imgCombo.sprite = spriteListCombo.listSprite[combolevel-1]
	imgComboCoef.sprite = spriteListComboCoef.listSprite[combolevel-1]
	imgComboCoefDot.sprite = spriteListComboCoefDot.listSprite[combolevel-1]
	--判断数字位数和字符
	local comboStr = tostring(comboNum)
	local strcount = string.len(comboStr)
	print(comboNum..' '..strcount)
	if strcount == 1 then
		imgComboNum1.sprite = spriteListComboNum.listSprite[(combolevel-1)*10 +comboNum]
		ImgComboNum2:SetActive(false)
		ImgComboNum3:SetActive(false)
	end
	if strcount == 2 then
		local ten = math.modf(comboNum/10)
		local one = math.modf(comboNum - 10 * ten)
		imgComboNum2.sprite = spriteListComboNum.listSprite[(combolevel-1)*10 +ten]
		imgComboNum1.sprite = spriteListComboNum.listSprite[(combolevel-1)*10 +one]
		ImgComboNum2:SetActive(true)
		ImgComboNum3:SetActive(false)
	end
	if strcount == 3 then
		local hundred = math.modf(comboNum/100)
		local ten = math.modf((comboNum- 100 * hundred)/10)
		local one = math.modf(comboNum - (100 * hundred) - (10 * ten))
		imgComboNum3.sprite = spriteListComboNum.listSprite[(combolevel-1)*10 +hundred]
		imgComboNum2.sprite = spriteListComboNum.listSprite[(combolevel-1)*10 +ten]
		imgComboNum1.sprite = spriteListComboNum.listSprite[(combolevel-1)*10 +one]
		ImgComboNum2:SetActive(true)
		ImgComboNum3:SetActive(true)
	end
	--倍率系数
	
	local one, minor
	one, minor = math.modf(coef)
	minor = math.modf(minor * 10)
	imgComboCoefNum1.sprite = spriteListComboCoefText.listSprite[(combolevel-1)*10 + one]
	imgComboCoefNum2.sprite = spriteListComboCoefText.listSprite[(combolevel-1)*10 + minor]
end
function UpdateFever(feverCount)
	PlayerFeverValue = feverCount
	local feverpercent = PlayerFeverValue / feverValueLimit
	imgFever:DOFillAmount(feverpercent,0.1) 
	textFeverCount.text = PlayerFeverValue..'/'..feverValueLimit
end
function UpdateScore()
	textScore.text = tostring(playerScore) 
end
function AddBuff(buffid)
	CS.GF.Battle.SkillUtils.GenBuff(
		CS.GF.Battle.BattleSkillCfgEx(skillbase, false, nil, nil),
		character.listMember[0],
		{buffid},
		{1},
		1
	)
end
function AddCreatorBuff(buffid)
	if creatorCharacter == nil then
		local friendlyTeamList = BattleController.friendlyTeamHolder.listCharacter
		for i=0, friendlyTeamList.Count-1 do
			local char = friendlyTeamList[i]
			if char:IsSummon() and char.gun.summonInfo.id == 1631 then
				creatorCharacter = char
				break
			end
		end
	end
	if creatorCharacter ~= nil then
		CS.GF.Battle.SkillUtils.GenBuff(
			CS.GF.Battle.BattleSkillCfgEx(skillbase, false, nil, nil),
			creatorCharacter.listMember[0],
			{buffid},
			{1},
			1
		)
	end
end
function GameFinish()
	print("GameSet!")
	CS.BattleFrameManager.StopTime(true,99999)
	--showPanel
	isGameFinish = true
	ShowResult()
end
function EndGame()
	
	xlua.hotfix(CS.GF.Battle.BattleCharacterController,'Die',nil)
	for i=BattleController.enemyTeamHolder.listCharacter.Count-1,0,-1 do
		local DamageInfo = CS.GF.Battle.BattleDamageInfo()
		BattleController.enemyTeamHolder.listCharacter[i]:UpdateLife(DamageInfo, -999999)
	end
	CS.BattleFrameManager.ResumeTime()
	CS.UnityEngine.Object.Destroy(GoResult)
	CS.UnityEngine.Object.Destroy(self.gameObject)
end


--local deathFlag = false
local deathFunctionFlag = false
local winFunctionFlag = false

function ShowResult()
	GoResult:SetActive(true)
	if feverEffectObj ~= nil then
		feverEffectObj:SetActive(false)
	end
	if comboEffectObj1 ~= nil then
		comboEffectObj1:SetActive(false)
	end
	if comboEffectObj2 ~= nil then
		comboEffectObj2:SetActive(false)
	end
	if comboEffectObj3 ~= nil then
		comboEffectObj3:SetActive(false)
	end
	OrderResultScoreAnim(GetRank())
	if CS.GameData.userInfo ~= nil then
		TextResultName:GetComponent(typeof(CS.ExText)).text = CS.GameData.userInfo.name
		TextResultID:GetComponent(typeof(CS.ExText)).text = CS.GameData.userInfo.userId
	end
	TextResultMaxCombo:GetComponent(typeof(CS.ExText)).text = playerMaxCombo 
	TextResultScore:GetComponent(typeof(CS.ExText)).text = playerScore
	TextResultMelon1:GetComponent(typeof(CS.ExText)).text = melonBreakCount[1]
	TextResultMelon2:GetComponent(typeof(CS.ExText)).text = melonBreakCount[2]
	TextResultMelon3:GetComponent(typeof(CS.ExText)).text = melonBreakCount[3]
	TextResultMelon4:GetComponent(typeof(CS.ExText)).text = melonBreakCount[4]
	TextResultMelon5:GetComponent(typeof(CS.ExText)).text = melonBreakCount[5]
	TextResultMelon6:GetComponent(typeof(CS.ExText)).text = melonBreakCount[6]
	TextResultMelon7:GetComponent(typeof(CS.ExText)).text = melonBreakCount[7]
	
end
function GetRank()
	if playerScore >= scoreRank4 then return 4 end
	if playerScore >= scoreRank3 then return 3 end
	if playerScore >= scoreRank2 then return 2 end
	return 1
end
function OrderResultScoreAnim(rank,percent)
	GoProgressBar.transform:Find("Img_LevelC").gameObject:GetComponent(typeof(CS.ExImage)).fillAmount = 0
	GoProgressBar.transform:Find("Img_LevelB").gameObject:GetComponent(typeof(CS.ExImage)).fillAmount = 0
	GoProgressBar.transform:Find("Img_LevelA").gameObject:GetComponent(typeof(CS.ExImage)).fillAmount = 0
	GoProgressBar.transform:Find("Img_LevelS").gameObject:GetComponent(typeof(CS.ExImage)).fillAmount = 0
	local seq = CS.DG.Tweening.DOTween.Sequence()
	if rank >= 1 then
		local amount = 1
		if rank == 1 then amount = (playerScore / scoreRank2) end
		seq:Append(GoProgressBar.transform:Find("Img_LevelC").gameObject:GetComponent(typeof(CS.ExImage)):DOFillAmount(amount,0.5))
	end
	if rank >= 2 then
		local amount = 1
		if rank == 2 then amount = (playerScore-scoreRank2)/(scoreRank3-scoreRank2) end
		seq:Append(GoProgressBar.transform:Find("Img_LevelB").gameObject:GetComponent(typeof(CS.ExImage)):DOFillAmount(amount,0.5))
	end
	if rank >= 3 then
		local amount = 1
		if rank == 3 then amount = (playerScore-scoreRank3)/(scoreRank4-scoreRank3) end
		seq:Append(GoProgressBar.transform:Find("Img_LevelA").gameObject:GetComponent(typeof(CS.ExImage)):DOFillAmount(amount,0.5))
	end
	if rank >= 4 then
		seq:Append(GoProgressBar.transform:Find("Img_LevelS").gameObject:GetComponent(typeof(CS.ExImage)):DOFillAmount(1,0.5))
	end
	ImgResultRank:GetComponent(typeof(CS.ExImage)).sprite = ImgResultRank:GetComponent(typeof(CS.UGUISpriteHolder)).listSprite[rank-1]
	seq:OnComplete(
		function()					
			TextResultScore:SetActive(true)
			ImgResultRank:SetActive(true)
			isResultPageAnimFinish = true
			PlaySFX("Stamp")
		end):Play()
end
function GetDate()
	local dtNow = CS.Data.ConvertDataTime(CS.GameData.GetCurrentTimeStamp())
	return dtNow:ToString("yyyy/MM/dd").." "..dtNow:ToString("HH:mm")
end
local Mathf = CS.UnityEngine.Mathf
local checkflag = false


function PlaySFX(FXname)
	if FXname == "HitNormal" then
		CS.CommonAudioController.PlayBattle("22Summer_WtaerMelon_Break")
	end
	if FXname == "HitIce" then
		CS.CommonAudioController.PlayBattle("22Summer_WtaerMelon_Ice_Break")
	end
	if FXname == "HitBomb" then
		CS.CommonAudioController.PlayBattle("22Summer_WtaerMelon_Bomb_Break")
	end
	if FXname == "HitNoBreak" then
		CS.CommonAudioController.PlayBattle("22Summer_WtaerMelon_Huge_Hit")		
	end
	if FXname == "HitHuge" then
		CS.CommonAudioController.PlayBattle("22Summer_WtaerMelon_Huge_Break")		
	end
	if FXname == "Move" then
		CS.CommonAudioController.PlayBattle("22Summer_Footstep")		
	end
	if FXname == "Stamp" then
		CS.CommonAudioController.PlayBattle("22Summer_Stamp")		
	end
end
--depose
OnDestroy =function()
	xlua.hotfix(CS.GF.Battle.BattleController,'RefreshFriendlyTargetList',nil)
	xlua.hotfix(CS.GF.Battle.BattleCharacterController,'Die',nil)
	xlua.hotfix(CS.GF.Battle.CSkillInstance,'_HandleMovementtEvent',nil)
	xlua.hotfix(CS.BattleMemberController,'PlaySkill',nil)
	character = nil
	mCurSkill ={}
end


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
xlua.private_accessible(CS.GF.Battle.gsEffect)
xlua.private_accessible(CS.GF.Battle.BattleSkillData)

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
local XBackMovePara = 1
local moveFowardID = 40540701
local moveBackID = 40540801
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
local thisFrameValue = nil
local skillActiveTimes = 0
local maxSkillActiveTimes = 7

local visionNear = 1.9
local visionFarBase = 3
local visionVerticalConf = 1
local visionRangeConf = 2.5
local visionLingerConf = 1.8
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
local moveSoundInterval = 0.6
local moveSoundFrameTimer = 4
local FP = CS.TrueSync.FP


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
local BattleDynamicData
--Awake：初始化数据
Awake = function()
	-- 关闭自动释放技能
	--textTime = TextTime:GetComponent(typeof(CS.ExText))
	BattleDynamicData = CS.GF.Battle.BattleDynamicData
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
	local SetVisible = function(self,visible)
		if self.mEffectObj ~= nil then
			self.mEffectObj:SetActive(visible)
		end
	end
	util.hotfix_ex(CS.GF.Battle.gsEffect,'SetVisible',SetVisible)
	util.hotfix_ex(CS.GF.Battle.BattleManager,'CheckBaseLine',CheckBaseLine)
	if CS.CommonAudioController.Instance.bgmSource ~= nil then
		CS.CommonAudioController.Instance.bgmSource:Stop()
	end
	if character == nil then
		character = CS.BattleLuaUtility.GetCharacterControllerNewByCode('Dandelion_M4')
		characterData = CS.BattleLuaUtility.GetDataByCode('Dandelion_M4')
	end
end
local haloObj


--Start: 加载组件
Start = function()
	--禁止人物拖动

	BattleController = CS.GF.Battle.BattleController.Instance
	CS.BattleInteractionController.isGuideInteractable = false
	CS.BattleInteractionController.isGuideCanNotScale = false
	CS.BattleInteractionController.isGuideCanNotOffset = false
	CS.GF.Battle.SkillUtils.AutoSkill = false	
	BattleController.resetAutoSkill = true
	BattleController.resetCameraLock = true
	BattleController.transform:Find("BattleField/CameraPositionDynamic/CameraPositionStatic/Main Camera/ShiningDust").gameObject:SetActive(false)
	haloObj = BattleController.transform:Find("Canvas/Halo").gameObject
	haloObj:SetActive(false)
	BattleController.transform:Find("Canvas/UI/SafeUIRect/DPSSwitch").gameObject:SetActive(false)
	BattleController.transform:Find("Canvas/DynamicCanvas/DPS").gameObject:SetActive(false)
	BattleController.transform:Find("Canvas/DynamicCanvas/TimerText").gameObject:SetActive(false)
	BattleController.transform:Find("Canvas/UI/Top/Top_Time").gameObject:SetActive(false)
	--注册相机
	self.transform:SetParent(CS.BattleUIController.Instance.transform:Find('UI'),false)
	--self:GetComponent('Canvas').worldCamera = CS.UnityEngine.Camera.main
	--注册人物
	

	if friendlyArea == nil then
		friendlyArea = BattleController.friendlyArea
		friendlyAreaInitalPos = friendlyArea.localPosition.x
	end
	character.reverseSync = true
	character.listMembers[0].mesh.sortingOrder = 3
	--character:SetMemberAnimation("wait", 1)
	--注册人物技能
	mCurSkill[1] = characterData:GetSkillByID(117602,true)
	mCurSkill[2] = characterData:GetSkillByID(117621,true)

	--mCurSkill[2] = character.gun:GetSkillByGroupId(406611)
	-- 人物扶正
	--character.listMember[0].transform.localEulerAngles = CS.UnityEngine.Vector3(0, 0, 0)
	
	-- 关闭自动技能 --------打完要记得调回去！（LoadAutoSkillPref）---------
	
	--countDown:GetComponent('Transform')
	--BtnTest:GetComponent('Button').onClick:AddListener(TestFunc)
	
	CS.BattleLuaUtility.SwitchUIManualPannel(false) -- 关闭手动技能面板
	CS.GF.Battle.BattleFrameManager.Register(UpdateJoyStick)
	JoyStick:GetComponent(typeof(CS.Joystick)).JoystickMoveHandle = JoyStickMove
	JoyStick:GetComponent(typeof(CS.Joystick)).JoystickEndHandle = JoyStickEnd
	JoyStick:GetComponent(typeof(CS.Joystick)).JoystickBeginHandle = JoyStickBegin
	

	--txCD = goCD:GetComponent('Text');
	--InitSkill1(SkillLabel1,mCurSkill[1],1)
	--InitSkill1(SkillLabel2,mCurSkill[2],2)
	BtnShimmer:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			ManualActiveSkill(mCurSkill[1])
		end)
	if not gameStartAnimFlag then
		JoyStick:SetActive(false)
		BtnShimmer:SetActive(false)
	end

end
UpdateJoyStick = function()
	if not gameStartAnimFlag then	
		MoveFront()
		--thisFrameJoyStick = false
		return
	end
	if gameEndAnimFlag then
		--thisFrameJoyStick = false
		return 
	end
	if cannotMoveFlag then
		if isMoving then
			isMoving = false
		end
		--thisFrameJoyStick = false
		return 
	end

	if thisFrameJoyStick then
		HandleJoyStickMove(thisFrameValue)
		
	else
		if isMoving then
			isMoving = false
			--print("wait1")
			character:SetMemberAnimation("wait", 1);
			moveSoundFrameTimer = 4
		end	
	end
end
Update = function()
	
	if friendlyArea ~= nil then
		local offset = friendlyArea.localPosition.x - friendlyAreaInitalPos
		local offsetFP = FP.FromFloat(offset)
		CS.GF.Battle.BattleDynamicData.friendlyArmyOffset = offsetFP
		--print(offset)
		--print(CS.GF.Battle.BattleDynamicData.friendlyArmyOffset)
	end
	if haloObj ~= nil and haloObj.activeSelf then
		haloObj:SetActive(false)
	end
	if mCurSkill[1] ~= nil then
		UpdateSkillUI(mCurSkill[1])
	end
	UpdateEnemyState()
	UpdateCreationState()
	if not lifebarFlag and character.lifeBar ~= nil then
		character.lifeBar.gameObject:SetActive(false)
		lifebarFlag = true
	end
	if not gameStartAnimFlag and characterData.conditionListSelf:GetTierByID(gameStartBuffID) > 0 then
		gameStartAnimFlag = true
		JoyStick:SetActive(true)
		JoyStick:GetComponent(typeof(CS.UnityEngine.CanvasGroup)).alpha = 0
		JoyStick:GetComponent(typeof(CS.UnityEngine.CanvasGroup)):DOFade(1,btnFadeInLeftDuration):SetDelay(btnFadeInLeftDelay)
		BtnShimmer:SetActive(true)
		BtnShimmer:GetComponent(typeof(CS.UnityEngine.CanvasGroup)).alpha = 0
		BtnShimmer:GetComponent(typeof(CS.UnityEngine.CanvasGroup)):DOFade(1,btnFadeInRightDuration):SetDelay(btnFadeInRightDelay)
		character.lifeBar.gameObject:SetActive(true)
		character.lifeBar.gameObject:GetComponent(typeof(CS.UnityEngine.CanvasGroup)).alpha = 0
		character.lifeBar.gameObject:GetComponent(typeof(CS.UnityEngine.CanvasGroup)):DOFade(1,lifebarFadeInDuration):SetDelay(lifebarFadeInDelay)
		if cooldownTween == nil then
			cooldownTween = GoShimmerAnim:GetComponent(typeof(CS.TweenPlay))
		end
		cooldownTween:DoTween()
		isMoving = false
		--print("wait2")
		character:SetMemberAnimation("wait", 1);
		moveSoundFrameTimer = 4
		--print("gameStartAnimFlag")
	end
	if not gameEndAnimFlag and characterData.conditionListSelf:GetTierByID(gameEndBuffID) > 0 then
		gameEndAnimFlag = true
		JoyStick:GetComponent(typeof(CS.UnityEngine.CanvasGroup)):DOFade(0,0.5):OnComplete(function()
				JoyStick:SetActive(false)
		end):Play()
		BtnShimmer:GetComponent(typeof(CS.UnityEngine.CanvasGroup)):DOFade(0,0.5):OnComplete(function()
				BtnShimmer:SetActive(false)
		end):Play()
		character.lifeBar.gameObject:GetComponent(typeof(CS.UnityEngine.CanvasGroup)):DOFade(0,0.5):OnComplete(function()
				BtnShimmer:SetActive(false)
			end):Play()
		--print("gameEndAnimFlag")
	end
	if characterData.conditionListSelf:GetTierByID(cannotMoveBuffID) > 0 then
		if not cannotMoveFlag then
			cannotMoveFlag = true
			--print("cannotMove")
		end
	else
		if cannotMoveFlag then 
			cannotMoveFlag = false
			--print("cannotMoveCancel")
		end
	end
	if blackBGTimer >=0 then
		blackBGTimer = blackBGTimer + CS.UnityEngine.Time.deltaTime
		if blackBGTimer >= blackBGDelay then
			blackBGTimer = -1
			HideBlackBG()
		end
	end
end
HideBlackBG = function()
	local upBlack = self.gameObject.transform:Find("BlackBackground/Img_Top")
	local downBlack = self.gameObject.transform:Find("BlackBackground/Img_Bottom")
	local totaltimeUp = (blackBGMoveUpperBound - upBlack.localPosition.y) / blackBGMoveSpeed
	local totaltimeDown = (blackBGMoveLowerBound - downBlack.localPosition.y) / blackBGMoveSpeed
	upBlack:DOLocalMoveY(blackBGMoveUpperBound,totaltimeUp)
	downBlack:DOLocalMoveY(blackBGMoveLowerBound,-totaltimeDown)
end
--depose
OnDestroy =function()
	CS.CommonAudioController.PlayBattle("21Summer_Field_Wind_Stop")
	CS.CommonAudioController.PlayBattle("GF_Halloween_Wind_loop_Stop")
	CS.CommonAudioController.PlayBattle("GF_Halloween_Femal_Cry_loop_Stop")
	CS.GF.Battle.BattleFrameManager.DeRegister(UpdateJoyStick)
	character = nil
	mCurSkill ={}
	xlua.hotfix(CS.GF.Battle.BattleManager,'CheckBaseLine',nil)
	xlua.hotfix(CS.GF.Battle.gsEffect,'SetVisible',nil)
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
	if input.eulerAngle >=0 + loss and input.eulerAngle < math.pi - loss then
		if isMoving then
			isMoving = false
			--print("wait3")
			character:SetMemberAnimation("wait", 1)
		end
		return 
	end
	local XPara = speedXPara
	local x =
	CS.Mathf.Clamp(
		character.transform.localPosition.x - math.sin(GetInputValue(input.eulerAngle)) * characterData.realtimeSpeed:AsFloat() * XPara * 1,
		minX,
		maxX
	)
	local y =
	CS.Mathf.Clamp(
		character.transform.localPosition.z + math.cos(GetInputValue(input.eulerAngle)) * characterData.realtimeSpeed:AsFloat() * speedYPara * 1,
		minY,
		maxY
	)
	--print(math.sin(input.eulerAngle))
	--print(math.cos(input.eulerAngle))
	--print("原始速度:"..character.realtimeSpeed .." ".."最终速度:"..character.gun.speed * XPara * input.value)
	
	local offset = CS.UnityEngine.Vector3(0, 0, y)
	if y == character.transform.localPosition.y then
		if isMoving then
			isMoving = false
			--print("wait4")
			character:SetMemberAnimation("wait", 1);
			moveSoundFrameTimer = 4
		end
	else 
		if isMoving == false then
			isMoving = true
			--print("move")
			character:SetMemberAnimation("spmove", 1);
		end
		moveSoundFrameTimer = moveSoundFrameTimer + 1
		if moveSoundFrameTimer >= 30 * moveSoundInterval then
			moveSoundFrameTimer = 0
			CS.CommonAudioController.PlayBattle("21Summer_Player_Move")
		end
	end
	
	character.transform.localPosition = offset
	if friendlyArea ~= nil then
		local startpos = friendlyArea.localPosition.x
		local movedistance = x
		if movedistance < 0  then  
			movedistance = 0 
		end
		local finalPos = startpos + movedistance
		friendlyArea.localPosition = CS.UnityEngine.Vector3(finalPos,friendlyArea.localPosition.y,friendlyArea.localPosition.z)
	end
end
MoveFront= function()
	if friendlyArea ~= nil then
		local startpos = friendlyArea.localPosition.x
		local movedistance = characterData.realtimeSpeed:AsFloat() * speedXPara * 1
		if movedistance < 0  then  
			movedistance = 0 
		end
		local finalPos = startpos + movedistance
		friendlyArea.localPosition = CS.UnityEngine.Vector3(finalPos,friendlyArea.localPosition.y,friendlyArea.localPosition.z)
	end
	if isMoving == false then
		isMoving = true
		--character.listMember[0]:PlaySkill(mCurSkill[2])
		--print(mCurSkill[2].info.id)
		--character:SetMemberAnimation("spmove", 1);
	end
	if characterData.realtimeSpeed:AsFloat() > 0 then
		moveSoundFrameTimer = moveSoundFrameTimer + 1
		if moveSoundFrameTimer >= 30 * moveSoundInterval then
			moveSoundFrameTimer = 0
			CS.CommonAudioController.PlayBattle("21Summer_Player_Move")
		end
	end
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
UpdateSkillUI = function(skill)
	
	if animTimer >= animDuration then
		animTimer = animDuration
	else
		animTimer = animTimer + CS.UnityEngine.Time.deltaTime
	end
	if cooldownTween == nil then
		cooldownTween = GoShimmerAnim:GetComponent(typeof(CS.TweenPlay))
	end
	if cooldownImage == nil then
		cooldownImage = GoShimmerAnim:GetComponent(typeof(CS.ExImage))
	end
	if skillActiveTimes >= maxSkillActiveTimes then
		cooldownImage.fillAmount = 0
		return
	end
	if skill.cdFrame:AsFloat() > 0 then
		cooldownTween:DoKill()
		cooldownImage.fillAmount = 1-(skill.cdFrame / skill.info.cdTime) 
		resetFlag = true
	else
		cooldownImage.fillAmount = 1
		if resetFlag then
			cooldownTween:DoTween()
			resetFlag = false
			if gameStartAnimFlag and not isMoving then
				--print("wait5")
				character:SetMemberAnimation("wait", 1)
			end
		end
	end
end

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
UpdateEnemyState = function()
	local enemyList = BattleController.listEnemyCharacterControllers
	for i=0,enemyList.Count-1 do
		local enemyCharacter = enemyList[i]
		local posSelf = character.listMembers[0].transform.position
		local posEnemy = enemyCharacter.listMembers[0].transform.position
		local distance = (posEnemy.x - posSelf.x)*(posEnemy.x - posSelf.x) + visionVerticalConf * visionVerticalConf * (posEnemy.z - posSelf.z)* (posEnemy.z - posSelf.z)
		for j=0,enemyCharacter.listMembers.Count-1 do
			local meshRenderer = enemyCharacter.listMembers[j].gameObject:GetComponent(typeof(CS.UnityEngine.MeshRenderer))
			if distance > GetVisionFar() * GetVisionFar() then
				meshRenderer.enabled = false
				meshRenderer.sortingOrder = 1
				enterFarDuration = 0
				enterNearDuration = 0
			else
				if enterFarDuration >= spineVisionFarDelay then
					meshRenderer.enabled = true
				else
					enterFarDuration = enterFarDuration + CS.UnityEngine.Time.deltaTime
				end
				if enemyCharacter.gun.info.code ~= 'unknown_minigame' and distance <= visionNear * visionNear then

					if enterNearDuration >= spineVisionNearDelay then
						meshRenderer.sortingOrder = 3
					else
						enterNearDuration = enterNearDuration + CS.UnityEngine.Time.deltaTime
						meshRenderer.sortingOrder = 1
					end
				else
					enterNearDuration = 0
					meshRenderer.sortingOrder = 1
				end
			end
			
		end

	end
end
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
		local posSelf = character.listMembers[0].transform.position
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

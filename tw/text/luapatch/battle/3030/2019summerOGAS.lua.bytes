local util = require 'xlua.util'
xlua.private_accessible(CS.CommonAudioController)
xlua.private_accessible(CS.CommonController)
xlua.private_accessible(CS.ResManager)
xlua.private_accessible(CS.BattleManualSkillController)
xlua.private_accessible(CS.GF.Battle.BattleDynamicData)
xlua.private_accessible(CS.GF.Battle.BattleCharacterControllerNew)
xlua.private_accessible(CS.GF.Battle.BattleCharacterData)
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
xlua.private_accessible(CS.GF.Battle.BattleFriendlyCharacterManager)
local FP = CS.TrueSync.FP
local character = nil
local characterData = nil
local mCurSkill ={}
local maxX = 5
local minX = -1
local maxY = 4
local minY = -6
local txCD = nil
--X分量的系数
local speedXPara = 0.02
--Y分量的系数
local speedYPara = 0.02
--后撤移动时的额外系数
local XBackMovePara = 0.8
local moveFowardID = 40540701
local moveBackID = 40540801
local cfgMoveFoward = nil
local cfgMoveBack = nil
local JoystickOffset
InitSkill1 = function(SkillLabel,mCurSkill,pos)
	local skillLabelController
    skillLabelController = SkillLabel:GetComponent(typeof(CS.BattleManualSkillController))
	--注册技能和人物
	skillLabelController:InitUI(characterData,pos-2,pos,0,mCurSkill,nil)
end

JoyStickMove = function(input)
	local XPara = speedXPara
	if input.value <= 0 then
		return
	end
	if input.eulerAngle < math.pi then
		XPara =XPara * XBackMovePara
		CS.GF.Battle.SkillUtils.GenBuffViaSkillConfig(characterData,moveFowardID,{-1})
		CS.GF.Battle.SkillUtils.GenBuffViaSkillConfig(characterData,moveBackID,{1})
		
	else
		CS.GF.Battle.SkillUtils.GenBuffViaSkillConfig(characterData,moveFowardID,{1})
		CS.GF.Battle.SkillUtils.GenBuffViaSkillConfig(characterData,moveBackID,{-1})

	end
	local friendPosX = CS.GF.Battle.BattleDynamicData.friendlyTeamHolder:GetLocalPos().x:AsFloat()
    local x =
        CS.Mathf.Clamp(
        character.data.characterPosition.x:AsFloat() - math.sin(input.eulerAngle) * characterData.realtimeSpeed:AsFloat() * XPara * input.value,
        minX,
        maxX
    )
    local y =
        CS.Mathf.Clamp(
        character.transform.localPosition.z + math.cos(input.eulerAngle) * characterData.realtimeSpeed:AsFloat() * speedYPara * input.value,
        minY,
        maxY
    )
	--print("友方区域位移:"..friendPosX )
	--JoystickOffset = CS.UnityEngine.Vector3(x , 0, y)
	character.data.characterPosition = CS.TrueSync.TSVector(FP.FromFloat(x) , FP.Zero, FP.FromFloat(y))
end

JoyStickBegin = function(input)
	
end

JoyStickEnd = function(input)
	--取消BUFF，代表角色停止移动
	CS.GF.Battle.SkillUtils.GenBuffViaSkillConfig(characterData,moveFowardID,{-1})
	CS.GF.Battle.SkillUtils.GenBuffViaSkillConfig(characterData,moveBackID,{-1})
end

TriggerInvincible = function()
	--增加一个Buff使得角色暂时无敌
	CS.GF.Battle.SkillUtils.GenBuffViaSkillConfig(characterData,40540601,nil,1)

end

--Awake：初始化数据
Awake = function()
    -- 关闭自动释放技能
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
	cfgMoveFoward = CS.GameData.listBTSkillCfg:GetDataById(moveFowardID)
	cfgMoveBack = CS.GameData.listBTSkillCfg:GetDataById(moveBackID)
	--注册相机
	self.transform:SetParent(CS.BattleUIController.Instance.transform:Find('UI'),false)
	--self:GetComponent('Canvas').worldCamera = CS.UnityEngine.Camera.main
	--注册人物
    if character == nil then
        character = CS.BattleLuaUtility.GetCharacterControllerNewByCode('M4A1Mod_Ogas')
		characterData = CS.BattleLuaUtility.GetDataByCode('M4A1Mod_Ogas')
    end
	--注册人物技能
    mCurSkill[1] = characterData:GetSkillByID(405403,true)
	mCurSkill[2] = characterData:GetSkillByID(405402,true)
	mCurSkill[3] = characterData:GetSkillByID(405405,true)
    -- 人物扶正
	--character.reverseSync = true
    character:ResetCharacterAngle(character.transform.localPosition)
    -- 修改碰撞盒
	character:InitCollider()

    CS.BattleLuaUtility.SwitchUIManualPannel(false) -- 关闭手动技能面板

    JoyStick:GetComponent(typeof(CS.Joystick)).JoystickMoveHandle = JoyStickMove
    JoyStick:GetComponent(typeof(CS.Joystick)).JoystickEndHandle = JoyStickEnd
    JoyStick:GetComponent(typeof(CS.Joystick)).JoystickBeginHandle = JoyStickBegin

    character.OnBarrageHit = TriggerInvincible
	InitSkill1(SkillLabel1,mCurSkill[1],1)
	InitSkill1(SkillLabel2,mCurSkill[2],2)
	InitSkill1(SkillLabel3,mCurSkill[3],3)
	
end
Update = function()

end
--depose
OnDestroy =function()
	character = nil
	mCurSkill ={}
end


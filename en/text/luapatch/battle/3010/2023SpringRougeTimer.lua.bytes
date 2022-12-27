local util = require 'xlua.util'
local config = require ('Battle/3010/2022ScarMinigameConfig')
xlua.private_accessible(CS.CommonAudioController)
xlua.private_accessible(CS.CommonController)
xlua.private_accessible(CS.ResManager)
xlua.private_accessible(CS.BattleManualSkillController)
xlua.private_accessible(CS.BattleMemberController)
xlua.private_accessible(CS.BattleFieldTeamHolder)
xlua.private_accessible(CS.BattleUILifeBarController)
xlua.private_accessible(CS.GF.Battle.BattleStatistics)
xlua.private_accessible(CS.GF.Battle.BattleStatistics)
xlua.private_accessible(CS.GF.Battle.EffectManager)
xlua.private_accessible(CS.GF.Battle.BattleConditionList)
xlua.private_accessible(CS.GF.Battle.CharacterCondition)

local timerText
local countdownTimer
local BattleController
--Awake：初始化数据
Awake = function()
	-- 关闭自动释放技能	
	
end


--Start: 加载组件
Start = function()
	--禁止人物拖动
	--CS.BattleScaler.maxNumber = 5
	BattleController = CS.GF.Battle.BattleController.Instance
	--BattleController.transform:Find("Canvas/UI/Top/Top_Time").gameObject:SetActive(false)
	BattleController.transform:Find("Canvas/DynamicCanvas/TimerText").gameObject:SetActive(false)
	self.transform:SetParent(CS.BattleUIController.Instance.transform:Find('UI'),false)
	timerText = txtTime:GetComponent(typeof(CS.ExText))
end


Update = function()
	
	countdownTimer = CS.BattleFrameManager.Instance:GetCurBattleTime()
	local countdownMinute = math.modf(countdownTimer / 60)
	local countdownSec = math.modf(countdownTimer - countdownMinute * 60) 
	timerText.text = string.format("%02d",(countdownMinute))..":"..string.format("%02d",(countdownSec))
end

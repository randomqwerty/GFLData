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
local isShown = false
local gameObject
local _textID,_textName,_textTime,_textStageName,_textDate
local btnClose
local showinfo = false
--Awake：初始化数据
Awake = function()
	-- 关闭自动释放技能	
	_textID = textUID:GetComponent(typeof(CS.ExText))
	_textName = textName:GetComponent(typeof(CS.ExText))
	_textTime = textTime:GetComponent(typeof(CS.ExText))
	_textStageName = textStageName:GetComponent(typeof(CS.ExText))
	_textDate = textDate:GetComponent(typeof(CS.ExText))
	BattleController = CS.GF.Battle.BattleController.Instance
	--BattleController.transform:Find("Canvas/UI/Top/Top_Time").gameObject:SetActive(false)
	--BattleController.transform:Find("Canvas/DynamicCanvas/TimerText").gameObject:SetActive(false)
	self.transform:SetParent(CS.BattleUIController.Instance.transform:Find('UI'),false)
	
	
	--timerText = txtTime:GetComponent(typeof(CS.ExText))
	btnBackGround:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			Exit()
		end)
	local RequestBattleFinish =  function(self,forcelose)
		if isShown then
			self:RequestBattleFinish(forcelose)
		else


			CS.BattleFrameManager.StopTime(true,9999999)
			ShowInfo()
		end
	end
	util.hotfix_ex(CS.GF.Battle.BattleController,'RequestBattleFinish',RequestBattleFinish)
	gameObject = self.gameObject
	gameObject:SetActive(false)
end


--Start: 加载组件
Start = function()
	--禁止人物拖动
	--CS.BattleScaler.maxNumber = 5
	
end


Update = function()
	
	
end
function ShowInfo()
	print("ShowInfo")
	gameObject:SetActive(true)
	if not showinfo then
		showinfo = true
	else
		return
	end
	if CS.GameData.userInfo ~= nil then
		_textName.text = CS.GameData.userInfo.name
		_textID.text = CS.GameData.userInfo.userId
	end
	if CS.GameData.currentSelectedMissionInfo ~= nil then
		_textStageName.text = CS.GameData.currentSelectedMissionInfo.name
	end
	
	countdownTimer = CS.BattleFrameManager.Instance:GetCurBattleTime()
	local countdownMinute = math.modf(countdownTimer / 60)
	local countdownSec = math.modf(countdownTimer - countdownMinute * 60) 
	local countdownRemain = countdownTimer - (countdownMinute * 60) - (countdownSec)
	_textTime.text = string.format("%02d",(countdownMinute))..":"..string.format("%02d",(countdownSec))..":"..string.format("%02d",(math.modf(countdownRemain*100)))
	_textDate.text = CS.GameData.UnixToDateTime(CS.GameData.GetCurrentTimeStamp()):ToString("yyyy/MM/dd HH:mm:ss");
end  
function Exit()
	isShown = true
	CS.UnityEngine.Time.timeScale = 1
	CS.BattleFrameManager.ResumeTime()
	CS.GF.Battle.BattleController.Instance:TriggerBattleFinishEvent()
	CS.UnityEngine.Object.Destroy(self.gameObject)
end
OnDestroy = function()
	xlua.hotfix(CS.GF.Battle.BattleController,'RequestBattleFinish',RequestBattleFinish)
end
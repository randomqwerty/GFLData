actionid = {1,2,3,4,5}
actionAnimCode = {"wait","wait","wait","wait","wait"} -- 每个动作对应的跳舞code
leaderSpineCode = "M1873"
dancerSpineCode = {"M1873","M1873","M1873","M1873","M1873","M1873","M1873"}--dancer1-7
npcSpecialAnimCode = "false"
npcSpecialAnimProp = 0.1 --npc特殊动作概率（每轮反馈每个npc都有此概率失败，如果失败，在这一轮的随机一个舞步上失败，播失败动作循环直到此轮结束）
yamadaFeverAnimCode = "fever"
npcFeverAnimCode = "surprise"
startingRandomRangeMin = 3 --起始随机下限
startingRandomRangeMax = 4 --起始随机上限

baseWaitTime = 10 --玩家基础操作时间
extraWaitTime = 0.5 --每有1个操作指令给予玩家的额外操作时间

------------------得分和fever相关参数---------------------
--得分每轮完成之后结算1次，得分=基础得分+时间得分
--基础得分：本轮每输入正确1个指令获得指令分，指令分与当前combo等级有关
--时间得分：本轮全部输入正确后，按照剩余时间得分，分数等于剩余时间乘以系数（取整）
--每次正确输入+1combo，错误输入combo清零

yamadaFailedAnimCode = "false" --主角失败动作
comboLvRequire = {0,15,30} --combo切阶段的要求
baseScore = {40,50,60} -- 指令基础得分
timeScoreCoef = 100 --时间分系数（单位：秒）

--每次正确输入积攒fever槽，fever满后切换到fever态，fever状态下连点计算combo且按照连点次数加分
feverGuageMax = 50
feverScoreCoef = 100 --fever状态下连点得分
feverDuration = 5 --fever持续时间（单位：秒）

------------------表现相关参数---------------------
--正常轮次：前置等待->领舞+玩家操作->npc反馈
--fever轮次：展示进入fever->玩家操控（连点）->展示离开fever
danceAnimFrame = {20,20,20,20,20} --舞蹈动作播放所需帧数 按照这个得出每轮领舞的舞步总时间（和spine动作对应）
preWaitTimeFrameFirstRound = 90 -- 第一轮开始玩家输入之前的等待时
preWaitTimeFrame = 30 -- 每轮开始玩家输入之前的等待时间
leadDanceExtraWaitFrame = 30 --领舞动作结束后转到玩家操作的额外等待时间（单位：帧）
playerDanceExtraWaitFrame = 30 --玩家舞蹈动作结束后转到下一轮的额外等待时间（单位：帧）
feverStartingFrame = 240 --fever前转场时间
feverEndingFrame = 240 --fever后转场时间

dictDanceRandRangeChange = {}
dictDancePreset = {} 
local configFunction = {}
function configFunction:InitData()
	--print(stageid)
	dictDancePreset[1] = {1,2,3,4,5}--配置第一轮动作
	dictDancePreset[2] = {1,2,0,4,5}--如果不是actionid的数字 则是1-5随机
	
	dictDanceRandRangeChange[3] = {3,5}--第三轮开始，将随机下限改为3，将随机上限改为5
end
return configFunction
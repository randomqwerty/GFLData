actionid = {1,2,3,4,5}
actionAnimCode = {"dance1","dance2","dance3","dance4","dance5"} -- 跳舞code随机列表,此动作不循环
danceAnimFrame = {34,28,22,41,29} --舞蹈动作播放所需帧数（和code一一对应，单位是帧数）
leaderSpineCode = "USAS12_2704"
dancerSpineCode = {"Sakura","Saki","Ai","Tae","Junko","Lily","Yuugiri"}--dancer1-7
npcSpecialAnimCode = "false"
npcSpecialAnimProp = 0.05 --npc特殊动作概率（每轮反馈每个npc都有此概率失败，如果失败，在这一轮的随机一个舞步上失败，播失败动作循环直到此轮结束）
yamadaFeverAnimCode = "fever"
npcFeverAnimCode = "surprise"
startingRandomRangeMin = 3 --起始随机下限
startingRandomRangeMax = 3 --起始随机上限

baseWaitTime = 2.5 --玩家基础操作时间
extraWaitTime = 0.2 --每有1个操作指令给予玩家的额外操作时间
totalTime = 90 --倒计时

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
feverGuageMax = 40
feverScoreCoef = 50 --fever状态下连点得分
feverDuration = 5 --fever持续时间（单位：秒）
scoreRanking = {0,3000,4500,6000} --到达C,B,A,S评价的分数要求
------------------表现相关参数---------------------
--正常轮次：前置等待->领舞+玩家操作->npc反馈
--fever轮次：展示进入fever->玩家操控（连点）->展示离开fever

preWaitTimeFrameFirstRound = 90 -- 第一轮开始玩家输入之前的等待时
preWaitTimeFrame = 5 -- 每轮开始玩家输入之前的等待时间
npcDanceDelay = 1-- 领舞和玩家跳舞的延迟（单位：帧）
--leadDanceExtraWaitFrame = 30 --领舞动作结束后转到玩家操作的额外等待时间（单位：帧）
playerDanceExtraWaitFrame = 30 --玩家舞蹈动作结束后转到下一轮的额外等待时间（单位：帧）
feverStartingFrame = 20 --fever前转场时间
feverEndingFrame = 20 --fever后转场时间

dictComboExtraStartingRangeDownCombo = {10,20,30,40,55}
dictComboExtraStartingRangeDownValue = {1,1,2,3,3} -- 根据combo值增加的额外随机下限

dictComboExtraStartingRangeUpCombo = {10,20,30,40,55}
dictComboExtraStartingRangeUpValue = {1,2,2,3,4} -- 根据combo值增加的额外随机上限


dictDanceRandRangeChange = {}
dictDancePreset = {} 
local configFunction = {}
function configFunction:InitData()
	--print(stageid)
	dictDancePreset[1] = {1,2,3}--配置第一轮动作 如果不是actionid的数字 则是1-5随机
	
	dictDanceRandRangeChange[4] = {3,4}--第三轮开始，将随机下限改为3，将随机上限改为5
	dictDanceRandRangeChange[8] = {4,4}

end
return configFunction
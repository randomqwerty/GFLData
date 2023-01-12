
totalTime = 90 --秒
cursorStartingPos = 0.0 -- 游标初始位置
cursorAscendCoef = 1.25 --游标上升时的最大速度（百分比/秒）
cursorDescendCoef = 1.5 --游标下降时的最大速度（百分比/秒）

cursorAscendAcc = 0.9 --游标上升时的加速度
cursorDescendAcc = 1 --游标下降时的加速度

cursorAscendStartingSpd = 0.6 --游标上升时的起始速度
cursorDescendStartingSpd = 0.35 --游标下降时的起始速度

baseScore = 10 --在范围内时，每次获得的分数数额

loseScoreLingerTime = 1 --离开范围多久后开始失分（秒）

loseScore = 10 --离开范围后，每次失去的分数数额

feverGuageMax = 50--fever满额要求
fevergain = 0.1--得分时获得fever
feverlose = 0.0--失分时失去fever

feverDuration = 5 --fever持续时间（秒）
feverScore = 100 --fever连点得分

startingRangePos = {0.2}
startingRangeWidth = {0.3}

dictRangeInfo = {} -- 音域信息合集，由3部分构成，关键时间，音域中心点，音域宽度
rangePosParameter = {} --音域中心点所在位置，填写1个数值时固定，2个数值时在上下限之间随机。若此值小于0则代表沿用上次的位置
rangeWidthParameter = {} --音域宽度，填写1个数值时固定，2个数值时在上下限之间随机（总宽度，在中心点两侧除以2）。若此值小于0则代表沿用上次的宽度
tableStruct = {}
configFunction = {}
nameList = {}
spineCodeList = {} --1-7
scoreRanking = {0,100,200,300} --到达C,B,A,S评价的分数要求
function configFunction:InitData()
	--print(stageid)
	--前一关键帧会朝着后面的关键帧补间变化，所以给定需要维持位置的话要写2次一样的内容，但关键帧不同，相当于持续x秒
	--默认的变化方式使用匀速
	nameList = {60631,60632,60633,60634,60635,60636,60637}
	spineCodeList = {"Sakura","Saki","Ai","Junko","Yuugiri","Lily","Tae"}
	rangePosParameter = {0.2}
	rangeWidthParameter = {0.3}
	tableStruct = {time = 0.8,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}
	dictRangeInfo[1] = tableStruct

	rangePosParameter = {0.8}
	rangeWidthParameter = {0.25}
	tableStruct = {time =  5.7,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --Earliest flowers of future bloom through twilight
	dictRangeInfo[2] = tableStruct

	rangePosParameter = {0.8}
	rangeWidthParameter = {0.25}
	tableStruct = {time =  6.1,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --Earliest flowers of future bloom through twilight
	dictRangeInfo[3] = tableStruct
	
	rangePosParameter = {0.4}
	rangeWidthParameter = {0.25}
	tableStruct = {time = 9.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --The train leaves away from a long tunnel of death
	dictRangeInfo[4] = tableStruct

	rangePosParameter = {0.8}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 10.8,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}  --The train leaves away from a long tunnel of death
	dictRangeInfo[5] = tableStruct

	rangePosParameter = {0.75}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 11.3,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --The train leaves away from a long tunnel of death
	dictRangeInfo[6] = tableStruct

	rangePosParameter = {0.9}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 13.8,pos = rangePosParameter, width = rangeWidthParameter,easeType = 8}  --Who’s paying the freight
	dictRangeInfo[7] = tableStruct

	rangePosParameter = {0.35}
	rangeWidthParameter = {0.25}
	tableStruct = {time = 16.8,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --Who else knows wrong or right
	dictRangeInfo[8] = tableStruct

	rangePosParameter = {0.8}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 19,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --We are gonna be alright alright
	dictRangeInfo[9] = tableStruct

	rangePosParameter = {0.75}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 19.3,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --We are gonna be alright alright
	dictRangeInfo[10] = tableStruct

	rangePosParameter = {0.9}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 20.4,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --We are gonna be alright alright
	dictRangeInfo[11] = tableStruct
		
	rangePosParameter = {0.85}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 20.7,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --We are gonna be alright alright
	dictRangeInfo[12] = tableStruct

	rangePosParameter = {0.15}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 25.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --We are gonna be alright alright
	dictRangeInfo[13] = tableStruct

	rangePosParameter = {0.8}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 28.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --
	dictRangeInfo[14] = tableStruct

	rangePosParameter = {0.2}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 31.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --
	dictRangeInfo[15] = tableStruct
	
	rangePosParameter = {0.8}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 34.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --
	dictRangeInfo[16] = tableStruct

	rangePosParameter = {0.2}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 37.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --
	dictRangeInfo[17] = tableStruct

	rangePosParameter = {0.8}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 40.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --
	dictRangeInfo[18] = tableStruct

	rangePosParameter = {0.2}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 43.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --
	dictRangeInfo[19] = tableStruct

	rangePosParameter = {0.8}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 46.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --
	dictRangeInfo[20] = tableStruct

	rangePosParameter = {0.2}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 49.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --
	dictRangeInfo[21] = tableStruct
	
	rangePosParameter = {0.8}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 52.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --
	dictRangeInfo[22] = tableStruct

	rangePosParameter = {0.2}
	rangeWidthParameter = {0.2}
	tableStruct = {time = 55.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 0}  --
	dictRangeInfo[23] = tableStruct
end
return configFunction

totalTime = 90 --秒
cursorStartingPos = 0.2 -- 游标初始位置
cursorAscendCoef = 1.25 --游标上升时的最大速度（百分比/秒）
cursorDescendCoef = 1.5 --游标下降时的最大速度（百分比/秒）

cursorAscendAcc = 0.9 --游标上升时的加速度
cursorDescendAcc = 1 --游标下降时的加速度

cursorAscendStartingSpd = 0.6 --游标上升时的起始速度
cursorDescendStartingSpd = 0.35 --游标下降时的起始速度

baseScore = 10 --在范围内时，每次获得的分数数额

loseScoreLingerTime = 1 --离开范围多久后开始失分（秒）

loseScore = 10 --离开范围后，每次失去的分数数额

feverGuageMax = 100--fever满额要求
fevergain = 0.06--得分时获得fever
feverlose = 0.0--失分时失去fever

feverDuration = 5 --fever持续时间（秒）
feverScore = 250 --fever连点得分

startingRangePos = {0.2}
startingRangeWidth = {0.3}

dictRangeInfo = {} -- 音域信息合集，由3部分构成，关键时间，音域中心点，音域宽度
rangePosParameter = {} --音域中心点所在位置，填写1个数值时固定，2个数值时在上下限之间随机。若此值小于0则代表沿用上次的位置
rangeWidthParameter = {} --音域宽度，填写1个数值时固定，2个数值时在上下限之间随机（总宽度，在中心点两侧除以2）。若此值小于0则代表沿用上次的宽度
tableStruct = {}
configFunction = {}
nameList = {}
spineCodeList = {} --1-7
scoreRanking = {5000,10000,15000,20000} --到达C,B,A,S评价的分数要求
function configFunction:InitData()
	--print(stageid)
	--前一关键帧会朝着后面的关键帧补间变化，所以给定需要维持位置的话要写2次一样的内容，但关键帧不同，相当于持续x秒
	--默认的变化方式使用匀速
	nameList = {60631,60632,60633,60634,60635,60636,60637}
	spineCodeList = {"Sakura","Saki","Ai","Junko","Yuugiri","Lily","Tae"}
	rangePosParameter = {0.2}
	rangeWidthParameter = {0.3}
	tableStruct = {time =0.8,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[1] = tableStruct
	
	rangePosParameter = {0.7}
	rangeWidthParameter = {0.2}
	tableStruct = {time =2.6,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[2] = tableStruct
	
	rangePosParameter = {0.7}
	rangeWidthParameter = {0.2}
	tableStruct = {time =2.7,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[3] = tableStruct
	
	rangePosParameter = {0.3}
	rangeWidthParameter = {0.3}
	tableStruct = {time =4.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[4] = tableStruct
	
	rangePosParameter = {0.3}
	rangeWidthParameter = {0.3}
	tableStruct = {time =4.6,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[5] = tableStruct
	
	rangePosParameter = {0.7}
	rangeWidthParameter = {0.2}
	tableStruct = {time =6.4,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[6] = tableStruct
	
	rangePosParameter = {0.7}
	rangeWidthParameter = {0.2}
	tableStruct = {time =6.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[7] = tableStruct
	
	rangePosParameter = {0.3}
	rangeWidthParameter = {0.3}
	tableStruct = {time =8.3,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[8] = tableStruct
	
	rangePosParameter = {0.3}
	rangeWidthParameter = {0.3}
	tableStruct = {time =8.4,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[9] = tableStruct
	
	rangePosParameter = {0.75,0.85}
	rangeWidthParameter = {0.2,0.3}
	tableStruct = {time =9.6,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[10] = tableStruct
	
	rangePosParameter = {0.15,0.25}
	rangeWidthParameter = {0.2,0.3}
	tableStruct = {time =10.8,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[11] = tableStruct
	
	rangePosParameter = {0.75,0.85}
	rangeWidthParameter = {0.2,0.3}
	tableStruct = {time =12,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[12] = tableStruct
	
	rangePosParameter = {0.15,0.25}
	rangeWidthParameter = {0.2,0.3}
	tableStruct = {time =13.2,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[13] = tableStruct
	
	rangePosParameter = {0.4,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =14,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[14] = tableStruct
	
	rangePosParameter = {0,0.6}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =15.4,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[15] = tableStruct
	
	rangePosParameter = {0.6,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =16.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[16] = tableStruct
	
	rangePosParameter = {0,0.6}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =18,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[17] = tableStruct
	
	rangePosParameter = {0.4,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =19.7,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[18] = tableStruct
	
	rangePosParameter = {0,0.6}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =21.2,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[19] = tableStruct
	
	rangePosParameter = {0.4,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =22.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[20] = tableStruct
	
	rangePosParameter = {0,0.6}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =23.7,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[21] = tableStruct
	
	rangePosParameter = {0.4,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =25.4,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[22] = tableStruct
	
	rangePosParameter = {0,0.6}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =26.6,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[23] = tableStruct
	
	rangePosParameter = {0.4,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =28.2,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[24] = tableStruct
	
	rangePosParameter = {0,0.6}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =29.7,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[25] = tableStruct
	
	rangePosParameter = {0.85}
	rangeWidthParameter = {0.2}
	tableStruct = {time =31.2,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[26] = tableStruct
	
	rangePosParameter = {0.84}
	rangeWidthParameter = {0.2}
	tableStruct = {time =31.3,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[27] = tableStruct
	
	rangePosParameter = {0.86}
	rangeWidthParameter = {0.2}
	tableStruct = {time =31.4,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[28] = tableStruct
	
	rangePosParameter = {0.84}
	rangeWidthParameter = {0.2}
	tableStruct = {time =31.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[29] = tableStruct
	
	rangePosParameter = {0.86}
	rangeWidthParameter = {0.2}
	tableStruct = {time =31.6,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[30] = tableStruct
	
	rangePosParameter = {0.84}
	rangeWidthParameter = {0.2}
	tableStruct = {time =31.7,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[31] = tableStruct
	
	rangePosParameter = {0.86}
	rangeWidthParameter = {0.2}
	tableStruct = {time =31.8,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[32] = tableStruct
	
	rangePosParameter = {0.84}
	rangeWidthParameter = {0.2}
	tableStruct = {time =31.9,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[33] = tableStruct
	
	rangePosParameter = {0.86}
	rangeWidthParameter = {0.2}
	tableStruct = {time =32,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[34] = tableStruct
	
	rangePosParameter = {0.84}
	rangeWidthParameter = {0.2}
	tableStruct = {time =32.1,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[35] = tableStruct
	
	rangePosParameter = {0.86}
	rangeWidthParameter = {0.2}
	tableStruct = {time =32.2,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[36] = tableStruct
	
	rangePosParameter = {0.84}
	rangeWidthParameter = {0.2}
	tableStruct = {time =32.3,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[37] = tableStruct
	
	rangePosParameter = {0.86}
	rangeWidthParameter = {0.2}
	tableStruct = {time =32.4,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[38] = tableStruct
	
	rangePosParameter = {0.84}
	rangeWidthParameter = {0.2}
	tableStruct = {time =32.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[39] = tableStruct
	
	rangePosParameter = {0.86}
	rangeWidthParameter = {0.2}
	tableStruct = {time =32.6,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[40] = tableStruct
	
	rangePosParameter = {0.84}
	rangeWidthParameter = {0.2}
	tableStruct = {time =32.7,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[41] = tableStruct
	
	rangePosParameter = {0.86}
	rangeWidthParameter = {0.2}
	tableStruct = {time =32.8,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[42] = tableStruct
	
	rangePosParameter = {0.84}
	rangeWidthParameter = {0.2}
	tableStruct = {time =32.9,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[43] = tableStruct
	
	rangePosParameter = {0.86}
	rangeWidthParameter = {0.2}
	tableStruct = {time =33,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[44] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =33.9,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[45] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =35.4,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[46] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =36.9,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[47] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =38.4,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[48] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =39.9,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[49] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =41.4,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[50] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =42.9,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[51] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =44.4,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[52] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =45.9,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[53] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =47.4,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[54] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =48.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[55] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =49.7,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[56] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =51.2,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[57] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =52.7,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[58] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =54.2,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[59] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =55.7,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[60] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =57.2,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[61] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =58.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[62] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =60.1,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[63] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =61.4,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[64] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =62.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[65] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =63.8,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[66] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.35}
	tableStruct = {time =65.1,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[67] = tableStruct
	
	rangePosParameter = {0.5}
	rangeWidthParameter = {0.35}
	tableStruct = {time =66.1,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[68] = tableStruct
	
	rangePosParameter = {0.5}
	rangeWidthParameter = {0.08}
	tableStruct = {time =73.1,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[69] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =74.4,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[70] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =75.7,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[71] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =77,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[72] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =78.3,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[73] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =79.6,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[74] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =80.9,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[75] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =82.2,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[76] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =83.5,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[77] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =84.8,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[78] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =86.1,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[79] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =87.4,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[80] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =88.7,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[81] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =90,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[82] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =91.3,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[83] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =92.6,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[84] = tableStruct
	
	rangePosParameter = {0,0.55}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =93.8999999999999,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[85] = tableStruct
	
	rangePosParameter = {0.45,1}
	rangeWidthParameter = {0.15,0.25}
	tableStruct = {time =95.1999999999999,pos = rangePosParameter, width = rangeWidthParameter,easeType = 2}
	dictRangeInfo[86] = tableStruct
	
end
return configFunction
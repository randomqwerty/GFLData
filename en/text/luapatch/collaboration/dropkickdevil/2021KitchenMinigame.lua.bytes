local util = require 'xlua.util'
xlua.private_accessible(CS.ResManager)
xlua.private_accessible(CS.TweenPlay)
xlua.private_accessible(CS.CommonAudioController)
xlua.private_accessible(CS.CommonController)
xlua.private_accessible(CS.BattleMemberController)
xlua.private_accessible(CS.BattleFieldTeamHolder)
xlua.private_accessible(CS.GF.Battle.BattleController)
xlua.private_accessible(CS.GF.Battle.BattleStatistics)
xlua.private_accessible(CS.BattleUIPauseController)
local TableStruct = nil
local TableStruct2 = nil
local TableStruct3 = nil
local TableStruct4 = nil
--暂停界面
local isUIPausing = false
--游戏时间暂停
local isPausing = false
local waitOpenResultPage = false
local isOpenResultPage = false
local isOpenResultPageCD = false
local openResultPageTimer = 0
local openResultPageTimer2 = 2

local stageNum = 5
local currentAvaliablePlayer = 2
local Player1Working = false
local Player2Working = false

local Player1Disable = false
local Player2Disable = false
local player1DisableTimer = 0
local player2DisableTimer = 0
local player1Spine
local player2Spine

local avaliableCookerNumber = 2
local playerCodeList = {}
local playerPosList = {}
local smokePosList = {}
local fullGuestList = {}
local stageGuestList = {}
local stageIngredientList = {}
local EventInfoList = {}

local stageInfo = {}
local stageCustomerInfo = {}
local waitingCustomerQueue = {}
local IngredientInfo = {}
local RecipeInfo = {}
local GuestInfo = {}
local EventPool = {}

local inited = false

local foodBGPicList
local foodPicList
local foodPicShineList
local resultEndlessPicList
local remarkPicList

local emojiListLv3 = {"Emoji__1203","Emoji__1205"}
local emojiListLv2 = {"Emoji_0202","Emoji_1740"}
local emojiListLv1 = {"Emoji__1303","Emoji__1002"}
local emojiListFail = {"Emoji__0510","Emoji__0511"}

local endlessTimeInfo = {60,120,150,180,210,240,270,300,330,360,390,420,450,480,510,540,570,600}
local endlessScoreInfo = {900,1800,2250,2700,4200,4800,5400,6000,6600,7200,8600,9250,9900,10560,11220,11900,13700,15000}
local textTime
local customerLeaveMinus = -100
local customerPatienceBonus = {-10,-10,0,20}
local targetGunCode = "Jashinchan"

local isCooker1Cooking = false
local Cooker1Holding = 0
local isCooker2Cooking = false
local Cooker2Holding = 0

local GOSmoke1
local GOSmoke2

local currentScore = 0
local TargetScore = 2000
--Awake：初始化数据
Awake = function()
	--初始化随机数
	math.randomseed(tostring(os.time()):reverse():sub(1, 7))
	--厨子信息
	playerCodeList[1] = "Jashinchan_Cook"
	playerCodeList[2] = "CZ75_3005_Cook"
	playerCodeList[3] = "M1895"
	
	playerPosList[1] = CS.UnityEngine.Vector3(-119.6,-135.8,0)
	playerPosList[2] = CS.UnityEngine.Vector3(210.4,-132.3,0)
	playerPosList[3] = CS.UnityEngine.Vector3(-360.9,-100.6,0)
	
	smokePosList[1] = CS.UnityEngine.Vector3(46,43,-4)
	smokePosList[2] = CS.UnityEngine.Vector3(356,43,-4)
	--关卡信息
	TableStruct2 = {1,2}
	TableStruct3 = {1}
	TableStruct  = {id = 1,enableIngredient = TableStruct2,enableDish = TableStruct3,cookerCnt = 1,playerCnt = 1, targetScore = 400, countdownTime = 75}
	stageInfo[TableStruct.id] = TableStruct 
	TableStruct2 = {1,2,3,4}
	TableStruct3 = {1,2}
	TableStruct  = {id = 2,enableIngredient = TableStruct2,enableDish = TableStruct3,cookerCnt = 1,playerCnt = 1, targetScore = 540, countdownTime = 120}
	stageInfo[TableStruct.id] = TableStruct 
	TableStruct2 = {1,2,3,4,5,6}
	TableStruct3 = {1,2,3}
	TableStruct  = {id = 3,enableIngredient = TableStruct2,enableDish = TableStruct3,cookerCnt = 2,playerCnt = 2, targetScore = 1260, countdownTime = 120}
	stageInfo[TableStruct.id] = TableStruct 
	TableStruct2 = {1,2,3,4,5,6}
	TableStruct3 = {1,2,3,4,5}
	TableStruct  = {id = 4,enableIngredient = TableStruct2,enableDish = TableStruct3,cookerCnt = 2,playerCnt = 2, targetScore = 2400, countdownTime = 180}
	stageInfo[TableStruct.id] = TableStruct 
	TableStruct2 = {1,2,3,4,5,6}
	TableStruct3 = {1,2,3,4,5}
	TableStruct  = {id = 5,enableIngredient = TableStruct2,enableDish = TableStruct3,cookerCnt = 2,playerCnt = 2, targetScore = 400, countdownTime = 0}
	stageInfo[TableStruct.id] = TableStruct 

	
	
	--初始化原材料信息
	--1 蔬菜 2土豆 3 鸡蛋 4 牛肉 5猪肉  6 米饭
	TableStruct = {id = 1, isEnable = false, isReady = false, isCooking = false, timer = 0,finishTime = 2,haveExtra = false,cookPlayer = 0}
	IngredientInfo[TableStruct.id] = TableStruct 
	TableStruct = {id = 2, isEnable = false, isReady = false, isCooking = false, timer = 0,finishTime = 2,haveExtra = false,cookPlayer = 0}
	IngredientInfo[TableStruct.id] = TableStruct 
	TableStruct = {id = 3, isEnable = false, isReady = false, isCooking = false, timer = 0,finishTime = 2,haveExtra = false,cookPlayer = 0}
	IngredientInfo[TableStruct.id] = TableStruct 
	TableStruct = {id = 4, isEnable = false, isReady = false, isCooking = false, timer = 0,finishTime = 4,haveExtra = false,cookPlayer = 0}
	IngredientInfo[TableStruct.id] = TableStruct 
	TableStruct = {id = 5, isEnable = false, isReady = false, isCooking = false, timer = 0,finishTime = 4,haveExtra = false,cookPlayer = 0}
	IngredientInfo[TableStruct.id] = TableStruct 
	TableStruct = {id = 6, isEnable = false, isReady = false, isCooking = false, timer = 0,finishTime = 2,haveExtra = false,cookPlayer = 0}
	IngredientInfo[TableStruct.id] = TableStruct 
	

	--初始化菜谱信息
	--1沙拉 2喜好烧 3咖喱 4牛肉盖饭  5 烤肉
	TableStruct2 = {1,2}
	TableStruct = {id = 1, isEnable = false, requireIngredient = TableStruct2, score = 80,finishTime = 4}
	RecipeInfo[TableStruct.id] = TableStruct
	
	TableStruct2 = {1,3,4}
	TableStruct = {id = 2, isEnable = false, requireIngredient = TableStruct2, score = 160,finishTime = 8}
	RecipeInfo[TableStruct.id] = TableStruct
	
	TableStruct2 = {2,5,6}
	TableStruct = {id = 3, isEnable = false, requireIngredient = TableStruct2, score = 140,finishTime = 6}
	RecipeInfo[TableStruct.id] = TableStruct
	
	TableStruct2 = {1,5,6}
	TableStruct = {id = 4, isEnable = false, requireIngredient = TableStruct2, score = 140,finishTime = 6}
	RecipeInfo[TableStruct.id] = TableStruct
	
	TableStruct2 = {1,2,4,5}
	TableStruct = {id = 5, isEnable = false, requireIngredient = TableStruct2, score = 220,finishTime = 10}
	RecipeInfo[TableStruct.id] = TableStruct
	
	--客人信息
	TableStruct2 = {0}
	TableStruct4 = {0}
	TableStruct3 = {-1}

	TableStruct = {id = 1, code = "Yurine", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = 0}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1}
	TableStruct3 = {-1}
	TableStruct4 = {100}
	TableStruct = {id = 2, code = "Medusa", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = 0}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {3}
	TableStruct3 = {-1}
	TableStruct4 = {100}
	TableStruct = {id = 3, code = "Pekora", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = 0}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {2}
	TableStruct3 = {-1}
	TableStruct4 = {100}
	TableStruct = {id = 4, code = "Minosu", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 5, patience3 = 5,missionInfo = TableStruct3, group = 0}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1}
	TableStruct3 = {5}
	TableStruct4 = {100}
	TableStruct = {id = 5, code = "M1903", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = 1}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1,2}
	TableStruct3 = {5}
	TableStruct4 = {40,60}
	TableStruct = {id = 6, code = "AN94", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = 1}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1,4,5}
	TableStruct3 = {5}
	TableStruct4 = {30,30,40}
	TableStruct = {id = 7, code = "KP31", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = 1}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1,2,3,4,5}
	TableStruct3 = {5}
	TableStruct4 = {20,20,20,20,20}
	TableStruct = {id = 8, code = "G11", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = 1}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1,2}
	TableStruct3 = {5}
	TableStruct4 = {70,30}
	TableStruct = {id = 9, code = "WA2000", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 10, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = 2}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1,3}
	TableStruct3 = {5}
	TableStruct4 = {50,50}
	TableStruct = {id = 10, code = "MP7", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 10, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = 2}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1,4}
	TableStruct3 = {5}
	TableStruct4 = {30,70}
	TableStruct = {id = 11, code = "95type", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 10, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = 2}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {3,5}
	TableStruct3 = {5}
	TableStruct4 = {50,50}
	TableStruct = {id = 12, code = "Python", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = 2}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {2,3}
	TableStruct3 = {5}
	TableStruct4 = {50,50}
	TableStruct = {id = 13, code = "MG4", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 10, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = 3}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {2,4}
	TableStruct3 = {5}
	TableStruct4 = {40,60}
	TableStruct = {id = 14, code = "AK12", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 10, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = 3}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {2,5}
	TableStruct3 = {5}
	TableStruct4 = {40,60}
	TableStruct = {id = 15, code = "K5", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = 3}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {2,3,4}
	TableStruct3 = {5}
	TableStruct4 = {30,40,30}
	TableStruct = {id = 16, code = "SPAS12", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 10, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = 3}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1}
	TableStruct3 = {-1}
	TableStruct4 = {100}
	TableStruct = {id = 17, code = "AN94", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1}
	TableStruct3 = {-1}
	TableStruct4 = {100}
	TableStruct = {id = 18, code = "KP31", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1}
	TableStruct3 = {-1}
	TableStruct4 = {100}
	TableStruct = {id = 19, code = "WA2000", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1}
	TableStruct3 = {-1}
	TableStruct4 = {100}
	TableStruct = {id = 20, code = "MP7", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1}
	TableStruct3 = {-1}
	TableStruct4 = {100}
	TableStruct = {id = 21, code = "95type", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {2}
	TableStruct3 = {-1}
	TableStruct4 = {100}
	TableStruct = {id = 22, code = "MG4", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 10, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {2}
	TableStruct3 = {-1}
	TableStruct4 = {100}
	TableStruct = {id = 23, code = "AK12", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 10, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1,2}
	TableStruct3 = {-1}
	TableStruct4 = {50,50}
	TableStruct = {id = 24, code = "MP7", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 10, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {2,3}
	TableStruct3 = {-1}
	TableStruct4 = {40,60}
	TableStruct = {id = 25, code = "SPAS12", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 10, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {2,3}
	TableStruct3 = {-1}
	TableStruct4 = {40,60}
	TableStruct = {id = 26, code = "Minosu", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 10, patience2 = 10, patience3 = 5,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1,2,3}
	TableStruct3 = {-1}
	TableStruct4 = {20,20,60}
	TableStruct = {id = 27, code = "G11", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct

	TableStruct2 = {1,2,3,4,5}
	TableStruct3 = {5}
	TableStruct4 = {20,20,20,20,20}
	TableStruct = {id = 28, code = "G11", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct

	TableStruct2 = {1,2,3,4,5}
	TableStruct3 = {5}
	TableStruct4 = {20,20,20,20,20}
	TableStruct = {id = 29, code = "G11", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct
	
	TableStruct2 = {1,2,3,4,5}
	TableStruct3 = {5}
	TableStruct4 = {20,20,20,20,20}
	TableStruct = {id = 30, code = "G11", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct

	TableStruct2 = {1,2,3,4,5}
	TableStruct3 = {5}
	TableStruct4 = {20,20,20,20,20}
	TableStruct = {id = 31, code = "G11", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct

	TableStruct2 = {1,2,3,4,5}
	TableStruct3 = {5}
	TableStruct4 = {20,20,20,20,20}
	TableStruct = {id = 32, code = "G11", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct

	TableStruct2 = {1,2,3,4,5}
	TableStruct3 = {5}
	TableStruct4 = {20,20,20,20,20}
	TableStruct = {id = 33, code = "G11", requireDishes = TableStruct2, requirePercent = TableStruct4, patience1 = 15, patience2 = 10, patience3 = 10,missionInfo = TableStruct3, group = -1}
	fullGuestList[TableStruct.id] = TableStruct
	
	--事件信息
	TableStruct2 = {des = "60156,60158",precheck = "0,0",effect = "11:5,15:1,16:2;15:1,16:3",endEventTitle = "60154,60154",endEventDes = "60157,60159"}
	TableStruct = {id = 1, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60154,eventDes = 60155, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60162,60164",precheck = "0,0",effect = "13:0,15:2,16:1;14:1,15:2,16:1",endEventTitle = "60160,60160",endEventDes = "60163,60165"}
	TableStruct = {id = 2, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60160,eventDes = 60161, isInital = false,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60168,60170",precheck = "3:50,0",effect = "1:50,17:0.25,15:2,16:1;11:5,15:2,16:1",endEventTitle = "60166,60166",endEventDes = "60169,60171"}
	TableStruct = {id = 3, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60166,eventDes = 60167, isInital = false,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {requireDish = 1,bonus = 80,effect = "0:0"}
	TableStruct = {id = 4, eventType = 1, eventTime = 30, punish = "0:0" ,eventTitle = 60277,eventDes = 60278, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60174,60176",precheck = "0,0",effect = "10:5;10:4",endEventTitle = "60172,60172",endEventDes = "60175,60177"}
	TableStruct = {id = 5, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60172,eventDes = 60173, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60174,60178",precheck = "0,0",effect = "10:5;10:2",endEventTitle = "60172,60172",endEventDes = "60175,60179"}
	TableStruct = {id = 6, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60172,eventDes = 60173, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60180,60176",precheck = "0,0",effect = "10:6;10:4",endEventTitle = "60172,60172",endEventDes = "60181,60177"}
	TableStruct = {id = 7, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60172,eventDes = 60173, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60182,60184",precheck = "0,0",effect = "10:1;10:3",endEventTitle = "60172,60172",endEventDes = "60183,60185"}
	TableStruct = {id = 8, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60172,eventDes = 60173, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60188,60190",precheck = "0,0",effect = "20:40;15:9,16:10",endEventTitle = "60186,60186",endEventDes = "60189,60191"}
	TableStruct = {id = 9, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60186,eventDes = 60187, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {requireDish = 4,bonus = 140, effect = "15:10,16:9"}
	TableStruct = {id = 10, eventType = 1, eventTime = 30, punish = "11:5" ,eventTitle = 60279,eventDes = 60280, isInital = false,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60194,60196",precheck = "0,0",effect = "19:180,11:5;0:0",endEventTitle = "60192,60192",endEventDes = "60195,60197"}
	TableStruct = {id = 11, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60192,eventDes = 60193, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60200,60202",precheck = "3:50,0",effect = "1:50,8:1;8:1,15:12,16:13",endEventTitle = "60198,60198",endEventDes = "60201,60203"}
	TableStruct = {id = 12, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60198,eventDes = 60199, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60206,60208",precheck = "0,3:50",effect = "11:5,15:13,16:12;1:50,15:13,16:12",endEventTitle = "60204,60204",endEventDes = "60207,60209"}
	TableStruct = {id = 13, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60204,eventDes = 60205, isInital = false,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60212,60214",precheck = "0,0",effect = "8:0.25;2:50",endEventTitle = "60210,60210",endEventDes = "60213,60215"}
	TableStruct = {id = 14, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60210,eventDes = 60211, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60218,60220",precheck = "0,0",effect = "11:5,17:0.5;15:15,16:16",endEventTitle = "60216,60216",endEventDes = "60219,60221"}
	TableStruct = {id = 15, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60216,eventDes = 60217, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60224,60226",precheck = "0,3:50",effect = "1:100,15:16,16:15;1:50,22:220,15:16,16:15",endEventTitle = "60222,60222",endEventDes = "60225,60227"}
	TableStruct = {id = 16, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60222,eventDes = 60223, isInital = false,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60230,60232",precheck = "0,0",effect = "11:5;10:1",endEventTitle = "60228,60228",endEventDes = "60231,60233"}
	TableStruct = {id = 17, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60228,eventDes = 60229, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60236,60238",precheck = "0,0",effect = "15:18,16:19;11:5",endEventTitle = "60234,60234",endEventDes = "60237,60239"}
	TableStruct = {id = 18, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60234,eventDes = 60235, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60242,60244",precheck = "0,0",effect = "11:5,15:19,16:18;14:2,15:19,16:18",endEventTitle = "60240,60240",endEventDes = "60243,60245"}
	TableStruct = {id = 19, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60240,eventDes = 60241, isInital = false,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60248,60250",precheck = "0,0",effect = "11:5;0:0",endEventTitle = "60246,60246",endEventDes = "60249,60251"}
	TableStruct = {id = 20, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60246,eventDes = 60247, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60248,60250",precheck = "0,0",effect = "11:5;0:0",endEventTitle = "60246,60246",endEventDes = "60249,60251"}
	TableStruct = {id = 21, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60246,eventDes = true, isInital = false,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60254,60256",precheck = "0,0",effect = "17:0.5,15:22,16:23;0:0",endEventTitle = "60252,60252",endEventDes = "60255,60257"}
	TableStruct = {id = 22, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60252,eventDes = 60253, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60267,60269",precheck = "0,0",effect = "11:5,15:23,16:22;15:23,16:22",endEventTitle = "60265,60265",endEventDes = "60268,60270"}
	TableStruct = {id = 23, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60265,eventDes = 60266, isInital = false,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60260,60262",precheck = "0,3:50",effect = "15:24,16:25;23:100",endEventTitle = "60258,60258",endEventDes = "60261,60262"}
	TableStruct = {id = 24, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60258,eventDes = 60259, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60267,60269",precheck = "0,0",effect = "11:5,15:25,16:24;15:25,16:24",endEventTitle = "60265,60265",endEventDes = "60268,60270"}
	TableStruct = {id = 25, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60265,eventDes = 60266, isInital = false,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
	TableStruct2 = {des = "60273,60275",precheck = "0,0",effect = "1:50;10:1",endEventTitle = "60271,60271",endEventDes = "60274,60276"}
	TableStruct = {id = 26, eventType = 2, eventTime = 30, punish = "0:0" ,eventTitle = 60271,eventDes = 60272, isInital = true,level = 3,eventDetail = TableStruct2}
	EventInfoList[TableStruct.id] = TableStruct
	
end
local btnPause
local btnRecipeOK
local btnRecipeClose
local btnRecipeReset
local btnEvent
local btnEventClose

local isRecipeOpen = false
local isEventOpen = false
local guestInterval = 15
local guestTimer = 10


local groupAInterval = 18
local groupBInterval = 18
local groupCInterval = 23
local groupDInterval = 19
local groupEInterval = 24
local groupATimer = -5 + groupAInterval
local groupBTimer = -11 + groupBInterval
local groupCTimer = -22 + groupCInterval
local groupDTimer = -180+ groupDInterval
local groupETimer = -360 + groupEInterval
local customerTimerRnd = 7

local globalTimer = 0
local timeLimit = 999

local OrderCustomer1
local OrderCustomer2
local OrderCustomer3
local OrderCustomer4

local CustomerSpine1
local CustomerSpine2
local CustomerSpine3
local CustomerSpine4

local order1WaitAnim = false
local order2WaitAnim = false
local order3WaitAnim = false
local order4WaitAnim = false


local CustomerLeft = CS.UnityEngine.Vector3(-1150,-230,0)
local CustomerRight = CS.UnityEngine.Vector3(1170,-230,0)
local CustomerPos1 = CS.UnityEngine.Vector3(-700,-110,0)
local CustomerPos2 = CS.UnityEngine.Vector3(-300,-110,0)
local CustomerPos3 = CS.UnityEngine.Vector3(300,-110,0)
local CustomerPos4 = CS.UnityEngine.Vector3(700,-110,0)

local currentEvent
local character
local curEndlessWave
--Start: 加载组件
Start = function()
	self.transform:SetParent(CS.BattleUIController.Instance.transform:Find('UI'),false)
	--暂停按钮
	btnPause = BtnPause:GetComponent(typeof(CS.ExButton))
	btnRecipeOK = BtnRecipeOK:GetComponent(typeof(CS.ExButton))
	btnRecipeClose = BtnRecipeClose:GetComponent(typeof(CS.ExButton))
	btnRecipeReset = BtnRecipeReset:GetComponent(typeof(CS.ExButton))
	btnEvent = BtnEvent:GetComponent(typeof(CS.ExButton))
	btnEventClose = BtnEventClose:GetComponent(typeof(CS.ExButton))
	textTime = TextTime:GetComponent(typeof(CS.ExText))
	btnPause.onClick:AddListener(
		function()
			PlaySFX("btn1")
			OnPauseButton()
		end)
	btnRecipeOK.onClick:AddListener(
		function()
			PlaySFX("btn1")
			EnsureCookDish()
		end)
	GoRecipe.transform:Find("Img_BlackBG").gameObject:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			CloseRecipePage()
		end)
	btnRecipeClose.onClick:AddListener(
		function()
			CloseRecipePage()
		end)
	btnRecipeReset.onClick:AddListener(
		function()
			PlaySFX("btnCancel")
			ClearCookDish()
		end)
	btnEvent.onClick:AddListener(
		function()
			OpenEventChoose()
		end)
	GOEventPage.transform:Find("Img_BlackBG").gameObject:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			CloseEventPage()
		end)
	btnEventClose.onClick:AddListener(
		function()
			CloseEventPage()
		end)
	TakeoutBtn1:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			OnClickTakeoutBtn(1)
		end)
	TakeoutBtn2:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			OnClickTakeoutBtn(2)
		end)
	TakeoutBtn3:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			OnClickTakeoutBtn(3)
		end)
	TakeoutBtn4:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			OnClickTakeoutBtn(4)
		end)
	TakeoutBtn5:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			OnClickTakeoutBtn(5)
		end)
	BtnContinue:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			PlaySFX("btn1")
			OnPauseButton()
		end)
	BtnExit:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			PlaySFX("btnCancel")
			ExitGame()
		end)
	BtnResult:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			if openResultPageTimer2 > 0 then
				return
			end
			PlaySFX("btn1")
			ClearGame()
		end)
	GoRecipe.transform:Find("Main/Img_BackgroundL").gameObject:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
		function()
			CS.CommonController.LightMessageTips(GetName(60282))
		end)
	--初始化关卡信息
	if character == nil then
		character = CS.BattleLuaUtility.GetCharacterByCode(targetGunCode)
		local BuffTier = character.conditionListSelf:GetTierByID(4449)
		print(BuffTier)
		if BuffTier > 0 and BuffTier <= 5 then
			stageNum = BuffTier
		end		
	end
	--stageNum = 5
	print("curstageinfo "..stageNum)
	local curstageinfo = stageInfo[stageNum]
	currentAvaliablePlayer = curstageinfo.playerCnt
	avaliableCookerNumber = curstageinfo.cookerCnt
	for i = 1,#curstageinfo.enableIngredient do
		stageIngredientList[i] = curstageinfo.enableIngredient[i]
	end
	for i = 1,#curstageinfo.enableDish do
		RecipeInfo[curstageinfo.enableDish[i]].isEnable = true
	end
	if stageNum ~= 5 then
		SetTargetScore(curstageinfo.targetScore,true)
		timeLimit = curstageinfo.countdownTime
	else
		curEndlessWave = 1
		SetTargetScore(GetEndlessScore(curEndlessWave),true)
		timeLimit = GetEndlessTime(curEndlessWave)
	end
	if stageNum == 1 then
		TableStruct2 = {id = 1, customerid = 2, customerdelay = 3, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 2, customerid = 5, customerdelay = 17, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 3, customerid = 17, customerdelay = 30, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 4, customerid = 18, customerdelay = 30, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 5, customerid = 19, customerdelay = 45, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 6, customerid = 20, customerdelay = 45, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 7, customerid = 5, customerdelay = 58, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 8, customerid = 17, customerdelay = 58, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 9, customerid = 2, customerdelay = 70, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 10, customerid = 17, customerdelay = 70, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2

	end
	if stageNum == 2 then
		TableStruct2 = {id = 1, customerid = 4, customerdelay = 5, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 2, customerid = 2, customerdelay = 20, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 3, customerid = 5, customerdelay = 25, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 4, customerid = 22, customerdelay = 35, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 5, customerid = 9, customerdelay = 40, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 6, customerid = 24, customerdelay = 50, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 7, customerid = 23, customerdelay = 55, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 8, customerid = 6, customerdelay = 65, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 9, customerid = 18, customerdelay = 70, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 10, customerid = 19, customerdelay = 80, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 11, customerid = 20, customerdelay = 85, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 12, customerid = 6, customerdelay = 95, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 13, customerid = 22, customerdelay = 95, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 14, customerid = 23, customerdelay = 100, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 15, customerid = 5, customerdelay = 105, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 16, customerid = 2, customerdelay = 115, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	

	end
	if stageNum == 3 then
		TableStruct2 = {id = 1, customerid = 3, customerdelay = 3, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 2, customerid = 6, customerdelay = 15, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 3, customerid = 9, customerdelay = 15, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 4, customerid = 13, customerdelay = 25, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 5, customerid = 18, customerdelay = 25, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 6, customerid = 21, customerdelay = 35, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 7, customerid = 26, customerdelay = 35, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 8, customerid = 2, customerdelay = 40, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 9, customerid = 23, customerdelay = 45, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 10, customerid = 25, customerdelay = 50, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 11, customerid = 10, customerdelay = 60, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 12, customerid = 6, customerdelay = 60, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 13, customerid = 9, customerdelay = 65, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 14, customerid = 13, customerdelay = 65, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 15, customerid = 5, customerdelay = 75, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 16, customerid = 26, customerdelay = 80, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 17, customerid = 13, customerdelay = 90, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 18, customerid = 9, customerdelay = 95, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 19, customerid = 23, customerdelay = 100, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 20, customerid = 25, customerdelay = 105, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 21, customerid = 27, customerdelay = 105, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 22, customerid = 2, customerdelay = 115, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 23, customerid = 18, customerdelay = 115, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
	end
	if stageNum == 4 then
		TableStruct2 = {id = 1, customerid = 5, customerdelay = 5, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 2, customerid = 10, customerdelay = 5, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 3, customerid = 5, customerdelay = 20, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 4, customerid = 9, customerdelay = 25, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 5, customerid = 10, customerdelay = 40, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 6, customerid = 11, customerdelay = 45, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 7, customerid = 12, customerdelay = 50, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 8, customerid = 14, customerdelay = 60, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2
		TableStruct2 = {id = 9, customerid = 8, customerdelay = 65, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 10, customerid = 28, customerdelay = 65, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 11, customerid = 29, customerdelay = 65, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 12, customerid = 6, customerdelay = 75, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 13, customerid = 15, customerdelay = 85, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 14, customerid = 12, customerdelay = 90, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 15, customerid = 7, customerdelay = 95, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 16, customerid = 16, customerdelay = 100, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 17, customerid = 8, customerdelay = 105, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 18, customerid = 30, customerdelay = 130, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 19, customerid = 31, customerdelay = 130, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 20, customerid = 32, customerdelay = 130, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 21, customerid = 33, customerdelay = 130, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 22, customerid = 3, customerdelay = 135, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 23, customerid = 2, customerdelay = 140, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 24, customerid = 15, customerdelay = 145, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 25, customerid = 14, customerdelay = 150, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 26, customerid = 11, customerdelay = 160, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 27, customerid = 8, customerdelay = 165, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 28, customerid = 8, customerdelay = 170, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
		TableStruct2 = {id = 29, customerid = 2, customerdelay = 175, isDone = false}
		stageCustomerInfo[TableStruct2.id] = TableStruct2	
	end
	--boss战斗特殊逻辑
	if stageNum == 4 then
		GoOrderBoss:SetActive(true)
		local spine = CS.UnityEngine.Object.Instantiate(CS.CommonController.GetSpinePrefab("Yurine"))
		spine.transform.localScale = CS.UnityEngine.Vector3(170,170,170)
		spine.transform:SetParent(GoOrderBoss.transform:Find("SpineHolder"),false)
		spine:SetActive(true)
		spine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, "wait", true, 0)
		spine:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = 15
	end
	--print(#stageCustomerInfo)
	--初始化关卡客人
	InitStageInfo()
	--初始化原料部分
	InitIngredient()
	--厨房
	InitCooker()
	--Order按钮
	InitCustomer()
	InitEventPool()
	InitScoreTable()
	SetScore(0)
	CS.BattleFrameManager.StopTime(true,99999)
	foodPicList = GoCooker1.transform:Find("Btn_Cook/Img_Food").gameObject:GetComponent(typeof(CS.UGUISpriteHolder)).listSprite
	foodBGPicList = GoCooker1.transform:Find("Btn_Cook/Img_FoodBK").gameObject:GetComponent(typeof(CS.UGUISpriteHolder)).listSprite
	resultEndlessPicList = ResultGO.transform:Find("Frame/Img_Level").gameObject:GetComponent(typeof(CS.UGUISpriteHolder)).listSprite
	foodPicShineList = GoDish1.transform:GetChild(0).gameObject:GetComponent(typeof(CS.UGUISpriteHolder)).listSprite
	remarkPicList = GoRecipeLeftList.transform:GetChild(0):Find("Remark").gameObject:GetComponent(typeof(CS.UGUISpriteHolder)).listSprite
	inited = true
	
end
--Update
local countDownFlag = true
local pausedTweenFlag = false
local stampflag = false
Update = function()
	if isOpenResultPageCD then
		openResultPageTimer2 = openResultPageTimer2 - CS.UnityEngine.Time.deltaTime
		if openResultPageTimer2 <= 0 then
			isOpenResultPageCD = false
		end
	end
	if isOpenResultPage then 
		if openResultPageTimer >= 0 then
			openResultPageTimer = openResultPageTimer + CS.UnityEngine.Time.deltaTime
		end
		if openResultPageTimer > 1.6 and stageNum ~= 5 and not stampflag then
			if currentScore >= TargetScore then
				ResultGO.transform:Find("Frame/Img_Passed").gameObject:SetActive(true)
				ResultGO.transform:Find("Frame/LevelBar/Img_A").gameObject:GetComponent(typeof(CS.ExImage)).fillAmount = 1
					
				PlaySFX("resultSuccess")
			else
				ResultGO.transform:Find("Frame/Img_Failed").gameObject:SetActive(true)
				ResultGO.transform:Find("Frame/LevelBar/Img_A").gameObject:GetComponent(typeof(CS.ExImage)).fillAmount = currentScore / TargetScore
				PlaySFX("resultFail")
			end
			stampflag = true
		end
		if openResultPageTimer >= 1.7 then
			PlaySFX("resultStamp")
			openResultPageTimer = -1
		end
		return 
	end
	UpdateEventWaitClose()
	UpdateRecipeWaitClose()
	UpdateIngredientCookingUI()	
	if IsPaused() then 
		if not pausedTweenFlag then
			TextTime:GetComponents(typeof(CS.TweenPlay))[1]:DoTween()
			pausedTweenFlag = true
		end
		return 
	end
	if pausedTweenFlag then
		TextTime:GetComponents(typeof(CS.TweenPlay))[1]:DoKill()
		pausedTweenFlag = false
	end
	globalTimer = globalTimer + CS.UnityEngine.Time.deltaTime
	UpdateIngredientCookingLogic()
	UpdateCookerLogic()
	UpdateStage()
	UpdateCustomer()
	UpdateEvent()

	local lastTime = timeLimit - globalTimer
	if lastTime < 0 then lastTime = 0 end
	local countdownMinute = math.modf(lastTime / 60)
	local countdownSec = math.modf(lastTime - countdownMinute * 60) 
	textTime.text = string.format("%02d",(countdownMinute))..":"..string.format("%02d",(countdownSec))
	if lastTime <= 10 and stageNum ~= 5 and countDownFlag then
		countDownFlag = false
		textTime.color = GenColor(240,35,92,255)
		TextTime:GetComponents(typeof(CS.TweenPlay))[0]:DoTween()
		--PlaySFX("CountDown")
	end
	if stageNum ~= 5 then
		if globalTimer >= timeLimit  then
			waitOpenResultPage = true
		end
	else
		if globalTimer >= timeLimit then
			CheckEndlessWave()
		end
	end
	if waitOpenResultPage and not isEventOpen and not isRecipeOpen then
		OpenResultPage()
	end
end

--暂停游戏
function OnPauseButton()
	isUIPausing = not isUIPausing
	if isUIPausing then
		CS.UnityEngine.Time.timeScale = 0
	else
		CS.UnityEngine.Time.timeScale = 1
	end
	--print(tostring(isUIPausing))
	PauseRefreshUI()
end

function IsPaused()
	return isUIPausing or isPausing
end
------------------Stage相关--------------------------
function InitStageInfo()
	local cnt = 1
	--根据客人总表创建关卡用到的客人表
	for i=1,#fullGuestList do
		local isStage = false
		for j =1, #fullGuestList[i].missionInfo do
			if fullGuestList[i].missionInfo[j] == stageNum then
				isStage = true
				break
			end
		end
		local fullTime = fullGuestList[i].patience1 + fullGuestList[i].patience2 + fullGuestList[i].patience3
		TableStruct = {id = cnt ,guestInfo = fullGuestList[i] ,RequestingMenu = 0,isRequesting = false ,timer = 0 ,requireTime = fullTime, requestNum = 0,orderpos = 0,patienceLevel = 3,isStage = isStage,
			 finalScore = 0, isWaitRequest = false}
		stageGuestList[cnt] = TableStruct
		cnt = cnt + 1	
	end
	--创建厨师Spine
	for i=1,currentAvaliablePlayer do
		local spine = CS.UnityEngine.Object.Instantiate(CS.CommonController.GetSpinePrefab(playerCodeList[i]))
		spine.transform.localScale = CS.UnityEngine.Vector3(170,170,170)
		spine.transform:SetParent(GoSpineHolderKitchen.transform,false)
		spine:SetActive(true)
		spine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, "wait", true, 0)
		spine:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = 13
		spine.transform.localPosition = playerPosList[i]
		if i == 1 then
			player1Spine = spine:GetComponent(typeof(CS.SkeletonAnimation))
		end
		if i == 2 then
			player2Spine = spine:GetComponent(typeof(CS.SkeletonAnimation))
		end
	end
	if currentAvaliablePlayer == 1 then
		GoAssistOne:SetActive(true)
		GoAssistTwo:SetActive(false)
	else
		GoAssistOne:SetActive(false)
		GoAssistTwo:SetActive(true)
		GoCookingEmpty:SetActive(false)
	end
end
--全局timer产生Order
function UpdateStage()
	for i = 1, #waitingCustomerQueue do
		if (OrderCustomer1 == nil and not order1WaitAnim) or (OrderCustomer2 == nil and not order2WaitAnim) or (OrderCustomer3 == nil and not order3WaitAnim) or (OrderCustomer4 == nil and not order4WaitAnim) then
			GenNewCustomerByid(waitingCustomerQueue[i])
			table.remove(waitingCustomerQueue,i)
			break
		end
	end
	groupETimer = groupETimer + CS.UnityEngine.Time.deltaTime
	if groupETimer >= groupEInterval then
		GenNewCustomer(3)
		groupETimer = math.random(-customerTimerRnd,customerTimerRnd)
	end
	groupDTimer = groupDTimer + CS.UnityEngine.Time.deltaTime
	if groupDTimer >= groupDInterval then
		GenNewCustomer(2)
		groupDTimer = math.random(-customerTimerRnd,customerTimerRnd)
	end
	groupCTimer = groupCTimer + CS.UnityEngine.Time.deltaTime
	if groupCTimer >= groupCInterval then
		GenNewCustomer(3)
		groupCTimer = math.random(-customerTimerRnd,customerTimerRnd)
	end
	groupBTimer = groupBTimer + CS.UnityEngine.Time.deltaTime
	if groupBTimer >= groupBInterval then
		GenNewCustomer(2)
		groupBTimer = math.random(-customerTimerRnd,customerTimerRnd)
	end
	groupATimer = groupATimer + CS.UnityEngine.Time.deltaTime
	if groupATimer >= groupAInterval then
		GenNewCustomer(1)
		groupATimer = math.random(-customerTimerRnd,customerTimerRnd)
	end
	if stageNum <= 4 then
		for i=1, #stageCustomerInfo do
			--print(globalTimer..' '..stageCustomerInfo[i].customerdelay..' '.. tostring(stageCustomerInfo[i].isDone))
			if (stageCustomerInfo[i].isDone == false) and stageCustomerInfo[i].customerdelay <= globalTimer then
				GenNewCustomerByid(stageCustomerInfo[i].customerid)
				stageCustomerInfo[i].isDone = true
			end
		end
	end
end
function GenNewCustomerByid(id)
	--print("GenNewCustomerByid "..id)
	
	local target = nil
	for i=1, #stageGuestList do
		--print(tostring(stageGuestList[i].isRequesting)..' '..stageGuestList[i].guestInfo.id)
		if not stageGuestList[i].isRequesting and stageGuestList[i].guestInfo.id == id then
			target = stageGuestList[i]
		end
	end
	if target == nil then
		--print("GenNewCustomerByidnotFound")
		return false
	end
	if (OrderCustomer1 ~= nil or order1WaitAnim) and (OrderCustomer2 ~= nil or order2WaitAnim) and (OrderCustomer3 ~= nil or order3WaitAnim) and (OrderCustomer4 ~= nil or order4WaitAnim) then
		EnqueueCustomer(target)
		return false
	end
	target.timer = -2.6 - 0.5
	if stageNum == 4 then
		target.timer = -0.1 - 0.5
	end
	target.patienceLevel = 3
	target.isRequesting = true
	target.isWaitRequest = false
	--随机需要的食物
	local randNum = math.random(1,100)
	local totalcnt = 0
	local requestNum = 1
	for i =1, #target.guestInfo.requireDishes do
		local weight = target.guestInfo.requirePercent[i]
		totalcnt = totalcnt + weight
		if randNum <= totalcnt then
			requestNum = target.guestInfo.requireDishes[i]
			break
		end
	end
	target.RequestingMenu = requestNum
	--分配到目前没在用的位子
	local avaliableList = {}
	local cnt = 1
	if OrderCustomer1 == nil then 
		avaliableList[cnt] = 1 
		cnt = cnt+1 
	end
	if OrderCustomer2 == nil then 
		avaliableList[cnt] = 2 
		cnt = cnt+1 
	end	
	if OrderCustomer3 == nil then 
		avaliableList[cnt] = 3 
		cnt = cnt+1 
	end
	if OrderCustomer4 == nil then 
		avaliableList[cnt] = 4 
		cnt = cnt+1 
	end
	if #avaliableList >= 1 then
		local randPos = avaliableList[math.random(1,#avaliableList)]
		target.orderpos = randPos
		if randPos == 1 then
			OrderCustomer1 = target
		end
		if randPos == 2 then
			OrderCustomer2 = target
		end
		if randPos == 3 then
			OrderCustomer3 = target
		end
		if randPos == 4 then
			OrderCustomer4 = target
		end
	end 
	--print("GenNewCustomer"..target.guestInfo.code..' '..target.RequestingMenu..' '..target.orderpos)
	if stageNum ~= 4 then
		GenCustomerSpine(target.guestInfo.code,target.orderpos)
	end
	InitOrderUI(target.orderpos)
	PlaySFX("newCustomer")
	return true
end
--派出一个新的客人
function GenNewCustomer(group)
	local cnt = 1
	local avaliableList = {}
	for i=1, #stageGuestList do
		if not stageGuestList[i].isRequesting and (stageGuestList[i].guestInfo.group == group or group == -1) and stageGuestList[i].isStage then
			avaliableList[cnt] = i
			cnt = cnt + 1
		end
	end
	if cnt == 1 then
		return false
	end
	local rnd = avaliableList[math.random(1,#avaliableList)]
	if (OrderCustomer1 ~= nil or order1WaitAnim) and (OrderCustomer2 ~= nil or order2WaitAnim) and (OrderCustomer3 ~= nil or order3WaitAnim) and (OrderCustomer4 ~= nil or order4WaitAnim) then
		EnqueueCustomer(stageGuestList[rnd])
		return false
	end
	stageGuestList[rnd].timer = -2.6
	stageGuestList[rnd].patienceLevel = 3
	stageGuestList[rnd].isRequesting = true
	--随机需要的食物
	local randNum = math.random(1,100)
	local totalcnt = 0
	local requestNum = 1
	for i =1, #stageGuestList[rnd].guestInfo.requireDishes do
		local weight = stageGuestList[rnd].guestInfo.requirePercent[i]
		totalcnt = totalcnt + weight
		if randNum <= totalcnt then
			requestNum = stageGuestList[rnd].guestInfo.requireDishes[i]
			break
		end
	end
	stageGuestList[rnd].RequestingMenu = requestNum
	--分配到目前没在用的位子
	avaliableList = {}
	cnt = 1
	if OrderCustomer1 == nil then 
		avaliableList[cnt] = 1 
		cnt = cnt+1 
	end
	if OrderCustomer2 == nil then 
		avaliableList[cnt] = 2 
		cnt = cnt+1 
	end	
	if OrderCustomer3 == nil then 
		avaliableList[cnt] = 3 
		cnt = cnt+1 
	end
	if OrderCustomer4 == nil then 
		avaliableList[cnt] = 4 
		cnt = cnt+1 
	end
	if #avaliableList >= 1 then
		local randPos = avaliableList[math.random(1,#avaliableList)]
		stageGuestList[rnd].orderpos = randPos
		if randPos == 1 then
			OrderCustomer1 = stageGuestList[rnd]
		end
		if randPos == 2 then
			OrderCustomer2 = stageGuestList[rnd]
		end
		if randPos == 3 then
			OrderCustomer3 = stageGuestList[rnd]
		end
		if randPos == 4 then
			OrderCustomer4 = stageGuestList[rnd]
		end
	end 
	--print("GenNewCustomer"..stageGuestList[rnd].guestInfo.code..' '..stageGuestList[rnd].RequestingMenu..' '..stageGuestList[rnd].orderpos)
	GenCustomerSpine(stageGuestList[rnd].guestInfo.code,stageGuestList[rnd].orderpos)
	InitOrderUI(stageGuestList[rnd].orderpos)
	PlaySFX("newCustomer")
	return true
	--RefreshOrderUI(stageGuestList[rnd].orderpos)
end
function EnqueueCustomer(customer)
	customer.isWaitRequest = true
	local flag = false
	for i=0,#waitingCustomerQueue do
		if waitingCustomerQueue[i] == -1 then
			waitingCustomerQueue[i] = customer.guestInfo.id
			flag = true
		end
	end
	if not flag then
		waitingCustomerQueue[#waitingCustomerQueue + 1] = customer.guestInfo.id
	end
end

------------------Ingredient相关---------------------
--cabbage =1 Potato = 2 Rice = 6,Egg = 3,Beef = 4,Pork = 5
local IngredientDealBuffList = {}
local IngredientDealMultiply = 0
function InitIngredient()

	for i = 1,#IngredientInfo do
		local flag = false
		for j=1,#stageIngredientList do
			if IngredientInfo[i].id == stageIngredientList[j] then
				flag = true
				break
			end
		end
		if flag then
			IngredientInfo[i].isEnable = true
			local ingredientObj = GoIngredientsLayout.transform:GetChild(i-1)
			ingredientObj.gameObject:SetActive(true)
			local t = i
			--print(ingredientObj.gameObject.name)
			--print(ingredientObj:Find("Btn_TouchArea").gameObject.name)
			ingredientObj:Find("Btn_TouchArea").gameObject:GetComponent(typeof(CS.ExButton)).onClick:AddListener(function()					
					OnselectIngredient(t)
				end)
		end
	end

end
function OnselectIngredient(id)
	if isUIPausing then return end
	local info = IngredientInfo[id]
	if isRecipeOpen then
		if info.isReady then
			PutIngredient(id)
			PlaySFX("ingredientSel")
		else
			if not info.isReady and not info.isCooking then
				if currentAvaliablePlayer > 0 then
					
					if not Player1Working and not Player1Disable then
						Player1Working = true
						info.cookPlayer = 1
						currentAvaliablePlayer = currentAvaliablePlayer -1
						info.isCooking = true
						--UpdatePlayerSpineAnim()
					else
						if not Player2Working and not Player2Disable then
							Player2Working = true
							info.cookPlayer = 2
							currentAvaliablePlayer = currentAvaliablePlayer -1
							info.isCooking = true
							--UpdatePlayerSpineAnim()
						end
					end
					if not info.isCooking then
						local curstageinfo = stageInfo[stageNum]
						local cnt = curstageinfo.playerCnt
						if Player1Disable then cnt = cnt -1 end
						CS.CommonController.LightMessageTips(string.gsub(GetName(60144),"{0}",tostring(cnt)))
					else			
						if id <= 2 then
							PlaySFX("ingredientCut")
						else
							PlaySFX("ingredientBoil")
						end
					end
				else
					PlaySFX("btn1")
					local curstageinfo = stageInfo[stageNum]
					local cnt = curstageinfo.playerCnt
					if Player1Disable then cnt = cnt -1 end
					CS.CommonController.LightMessageTips(string.gsub(GetName(60144),"{0}",tostring(cnt)))
				end
			end
		end
	else
		if info.isReady then
			CS.CommonController.LightMessageTips(GetName(60145))
			PlaySFX("btn1")
			return
		end
		if not info.isReady and not info.isCooking then
			if currentAvaliablePlayer > 0 then
				
				if not Player1Working and not Player1Disable then
					Player1Working = true
					info.cookPlayer = 1
					currentAvaliablePlayer = currentAvaliablePlayer -1
					info.isCooking = true
					--UpdatePlayerSpineAnim()
				else
					if not Player2Working and not Player2Disable then
						Player2Working = true
						info.cookPlayer = 2
						currentAvaliablePlayer = currentAvaliablePlayer -1
						info.isCooking = true
						--UpdatePlayerSpineAnim()
					end
				end
				if not info.isCooking then
					local curstageinfo = stageInfo[stageNum]
					local cnt = curstageinfo.playerCnt
					if Player1Disable then cnt = cnt -1 end
					CS.CommonController.LightMessageTips(string.gsub(GetName(60144),"{0}",tostring(cnt)))
				else			
					if id <= 2 then
						PlaySFX("ingredientCut")
					else
						PlaySFX("ingredientBoil")
					end
				end
			else
				PlaySFX("btn1")
				local curstageinfo = stageInfo[stageNum]
				local cnt = curstageinfo.playerCnt
				if Player1Disable then cnt = cnt -1 end
				CS.CommonController.LightMessageTips(string.gsub(GetName(60144),"{0}",tostring(cnt)))
			end
		end
	end

end
function GainExtraIngredient(type)
	if type < 1 or type > 6 then return end
	if IngredientInfo[type].isReady then
		IngredientInfo[type].haveExtra = true
	else
		if IngredientInfo[type].isCooking then
			FinishIngredientCooking(type)
		else
			IngredientInfo[type].isReady = true
		end
	end
	UpdateIngredientCookingUI()	
end
function FinishIngredientCooking(id)
	if IngredientInfo[id].isCooking then
		IngredientInfo[id].isCooking = false
		IngredientInfo[id].timer = 0
		IngredientInfo[id].isReady = true
		if IngredientInfo[id].cookPlayer == 1 then
			Player1Working = false
			if GoAssistOne.activeSelf then
				GoAssistOne.transform:GetChild(0):GetChild(0).gameObject:SetActive(true)
			else
				GoAssistTwo.transform:GetChild(0):GetChild(0).gameObject:SetActive(true)
			end
			--UpdatePlayerSpineAnim()
		end
		if IngredientInfo[id].cookPlayer == 2 then
			Player2Working = false
			GoAssistTwo.transform:GetChild(1):GetChild(0).gameObject:SetActive(true)
			--UpdatePlayerSpineAnim()
		end
		currentAvaliablePlayer  = currentAvaliablePlayer + 1	
	end
end
function AddIngredientbuff(arg,duration)
	local flag = true
	for i=1,#IngredientDealBuffList do
		if IngredientDealBuffList[i].timer >= IngredientDealBuffList[i].duration then
			
		end
		
	end
	
	if flag then
		TableStruct = {arg = arg,duration = duration,timer = 0}
		IngredientDealBuffList[#IngredientDealBuffList + 1] = TableStruct
	end
end
function UpdateIngredientbuff()
	IngredientDealMultiply = 0
	for i=1,#IngredientDealBuffList do
		IngredientDealBuffList[i].timer = IngredientDealBuffList[i].timer + CS.UnityEngine.Time.deltaTime
		if IngredientDealBuffList[i].timer < IngredientDealBuffList[i].duration then
			IngredientDealMultiply = IngredientDealMultiply + IngredientDealBuffList[i].arg
		end
		
	end
end
function UpdateIngredientCookingLogic()
	UpdateIngredientbuff()
	
	if Player1Disable then
		player1DisableTimer = player1DisableTimer - CS.UnityEngine.Time.deltaTime
		if player1DisableTimer <= 0  then
			Player1Disable = false
			if GoAssistOne.activeSelf then
				GoAssistOne.transform:GetChild(0):GetChild(1).gameObject:SetActive(false)
				if not Player1Working then
					GoAssistOne.transform:GetChild(0):GetChild(0).gameObject:SetActive(true)
				end
			else
				GoAssistTwo.transform:GetChild(0):GetChild(1).gameObject:SetActive(false)
				if not Player1Working then
					GoAssistTwo.transform:GetChild(0):GetChild(0).gameObject:SetActive(true)
				end
			end
			UpdatePlayerSpineAnim()
					
		end
	end
	if Player2Disable then
		player2DisableTimer = player2DisableTimer - CS.UnityEngine.Time.deltaTime
		if player2DisableTimer <= 0  then
			Player2Disable = false
			GoAssistTwo.transform:GetChild(1):GetChild(1).gameObject:SetActive(false)
			if not Player2Working then
				GoAssistTwo.transform:GetChild(1):GetChild(0).gameObject:SetActive(true)
			end
			UpdatePlayerSpineAnim()
		end
	end
	for i = 1,#IngredientInfo do
		if IngredientInfo[i].isCooking then
			if (IngredientInfo[i].cookPlayer == 1 and Player1Disable) or (IngredientInfo[i].cookPlayer == 2 and Player2Disable) then
				
			else
				IngredientInfo[i].timer = IngredientInfo[i].timer + (CS.UnityEngine.Time.deltaTime *(1+IngredientDealMultiply))
				if IngredientInfo[i].timer >= IngredientInfo[i].finishTime then
					FinishIngredientCooking(i)
				end
			end						
		end		
	end
	UpdateIngredientCookingUI()
end
function UpdateIngredientCookingUI()	
	for i = 1,#IngredientInfo do	

		if IngredientInfo[i].isEnable then
			local ingredientObj = GoIngredientsLayout.transform:GetChild(i-1)
			if not isRecipeOpen then
				ingredientObj:Find("RecipeMask").gameObject:SetActive(false)
			end
			if IngredientInfo[i].isCooking then
				ingredientObj:Find("Img_Progress").gameObject:GetComponent(typeof(CS.ExImage)).fillAmount = IngredientInfo[i].timer/IngredientInfo[i].finishTime
				
				if (IngredientInfo[i].cookPlayer == 1 and Player1Disable) or (IngredientInfo[i].cookPlayer == 2 and Player2Disable) then
					ingredientObj:Find("Img_Knife").gameObject:SetActive(false)
					ingredientObj:Find("Img_KnifeDisable").gameObject:SetActive(true)
				else
					ingredientObj:Find("Img_Knife").gameObject:SetActive(true)
					ingredientObj:Find("Img_KnifeDisable").gameObject:SetActive(false)
				end
			else 
				ingredientObj:Find("Img_Knife").gameObject:SetActive(false)
				if IngredientInfo[i].isReady then
					ingredientObj:Find("Img_Progress").gameObject:GetComponent(typeof(CS.ExImage)).fillAmount = 1
					--ingredientObj:Find("Img_Ingredients").gameObject:SetActive(true)
					ingredientObj:Find("Img_Ready").gameObject:SetActive(true)
					if isRecipeOpen then
						ingredientObj:Find("RecipeMask").gameObject:SetActive(true)
					end
				end
				if IngredientInfo[i].haveExtra then
					ingredientObj:Find("Additional").gameObject:SetActive(true)
					if isRecipeOpen then
						ingredientObj:Find("RecipeMask/Additional").gameObject:SetActive(true)
					end
				else
					ingredientObj:Find("Additional").gameObject:SetActive(false)
					if isRecipeOpen then
						ingredientObj:Find("RecipeMask/Additional").gameObject:SetActive(false)
					end
				end
			end
		end
	end
	if Player1Working then
		if GoAssistOne.activeSelf then
			GoAssistOne.transform:GetChild(0):GetChild(1).gameObject:SetActive(false)
			GoAssistOne.transform:GetChild(0):GetChild(0).gameObject:SetActive(false)
		else
			GoAssistTwo.transform:GetChild(0):GetChild(1).gameObject:SetActive(false)
			GoAssistTwo.transform:GetChild(0):GetChild(0).gameObject:SetActive(false)
		end
	else
		if Player1Disable then
			if GoAssistOne.activeSelf then
				GoAssistOne.transform:GetChild(0):GetChild(1).gameObject:SetActive(true)
				GoAssistOne.transform:GetChild(0):GetChild(0).gameObject:SetActive(false)
			else
				GoAssistTwo.transform:GetChild(0):GetChild(1).gameObject:SetActive(true)
				GoAssistTwo.transform:GetChild(0):GetChild(0).gameObject:SetActive(false)
			end
		else
			if GoAssistOne.activeSelf then
				GoAssistOne.transform:GetChild(0):GetChild(1).gameObject:SetActive(false)
				GoAssistOne.transform:GetChild(0):GetChild(0).gameObject:SetActive(true)
			else
				GoAssistTwo.transform:GetChild(0):GetChild(1).gameObject:SetActive(false)
				GoAssistTwo.transform:GetChild(0):GetChild(0).gameObject:SetActive(true)
			end
		end
	end

	if Player2Working then
		GoAssistTwo.transform:GetChild(1):GetChild(1).gameObject:SetActive(false)
		GoAssistTwo.transform:GetChild(1):GetChild(0).gameObject:SetActive(false)
	else
		if Player2Disable then
			GoAssistTwo.transform:GetChild(1):GetChild(1).gameObject:SetActive(true)
			GoAssistTwo.transform:GetChild(1):GetChild(0).gameObject:SetActive(false)
		else	
			GoAssistTwo.transform:GetChild(1):GetChild(1).gameObject:SetActive(false)
			GoAssistTwo.transform:GetChild(1):GetChild(0).gameObject:SetActive(true)
		end
	end
end
function UpdatePlayerSpineAnim()
	if isCooker1Cooking then
		if Player1Disable then
			player1Spine.state:AddAnimation(0, "damagedcook", true, 0)
		else
			player1Spine.state:AddAnimation(0, "cook", true, 0)
		end
	else
		if Player1Disable then
			player1Spine.state:AddAnimation(0, "damaged", true, 0)
		else
			player1Spine.state:AddAnimation(0, "wait", true, 0)
		end
	end
	if avaliableCookerNumber == 2 then
		if isCooker2Cooking then
			player2Spine.state:AddAnimation(0, "cook", true, 0)
		else
			player2Spine.state:AddAnimation(0, "wait", true, 0)
		end
	end
end
function ResumeIngredientCookingUI()

	for i = 1,#IngredientInfo do
		if IngredientInfo[i].isEnable then
			if not IngredientInfo[i].isReady then
				local ingredientObj = GoIngredientsLayout.transform:GetChild(i-1)
				if not IngredientInfo[i].isCooking then
					ingredientObj:Find("Img_Progress").gameObject:GetComponent(typeof(CS.ExImage)).fillAmount = 0
				end
				--ingredientObj:Find("Img_Ingredients").gameObject:SetActive(false)
				ingredientObj:Find("Img_Ready").gameObject:SetActive(false)
			end
		end
	end
end
function PauseRefreshUI()
	if isUIPausing then
		GOPause:SetActive(true)
	else
		GOPause:SetActive(false)
	end
end	
------------------Cooker相关---------------------


local cooker1Timer = 0
local cooker2Timer = 0

local cooker1TargetTime = 0
local cooker2TargetTime = 0
local currentSelectCooker = 0
local foodPos1 = 0
local foodPos2 = 0
local foodPos3 = 0


function InitCooker()
	if avaliableCookerNumber == 1 then
		GoCooker1:SetActive(true)
		SetCookerOn(GoCooker1,false)
		InitCookerEvent(GoCooker1,1)
	else
		GoCooker1:SetActive(true)
		SetCookerOn(GoCooker1,false)
		InitCookerEvent(GoCooker1,1)
		GoCooker2:SetActive(true)
		SetCookerOn(GoCooker2,false)
		InitCookerEvent(GoCooker2,2)
	end
	if GOSmoke1 == nil then
		GOSmoke1 = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Effect/Tieguo_yan"))
		GOSmoke1.transform:SetParent(GoSpineHolderKitchen.transform,false)
		GOSmoke1.transform.localPosition = smokePosList[1]
		GOSmoke1:SetActive(false)
	end
	if GOSmoke2 == nil then
		GOSmoke2 = CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("Effect/Tieguo_yan"))
		GOSmoke2.transform:SetParent(GoSpineHolderKitchen.transform,false)
		GOSmoke2.transform.localPosition = smokePosList[2]
		GOSmoke2:SetActive(false)
	end
end
function SetCookerOn(gameobject, isOn)
	gameobject.transform:Find("On").gameObject:SetActive(isOn)
	gameobject.transform:Find("Off").gameObject:SetActive(not isOn)
end
function InitCookerEvent(cookerObj, pos)
	cookerObj.transform:Find("Btn_Cook").gameObject:GetComponent(typeof(CS.ExButton)).onClick:AddListener(function()					
			OnSelectCooker(pos)
		end)
end
function OnSelectCooker(pos)

	if pos == 1 then
		if not isCooker1Cooking and Cooker1Holding == 0 then
			currentSelectCooker = pos
			OpenRecipe()
		else
			if isCooker1Cooking then
				CS.CommonController.LightMessageTips(GetName(60146))
			end
		end
	end
	if pos == 2 then
		if not isCooker2Cooking and Cooker2Holding == 0 then
			currentSelectCooker = pos
			OpenRecipe()
		else
			if isCooker2Cooking then
				CS.CommonController.LightMessageTips(GetName(60146))
			end
		end
	end
	if pos == -1 then
		if not isCooker1Cooking and Cooker1Holding == 0 then
			currentSelectCooker = 1
			OpenRecipe()
		else
			if avaliableCookerNumber == 2 and not isCooker2Cooking and Cooker2Holding == 0 then
				currentSelectCooker = 2
				OpenRecipe()
			else
				PlaySFX("btn1")
				CS.CommonController.LightMessageTips(GetName(60147))
			end
		end
		
	end
end
function CookDish(pos,dishID)
	if (pos == 1 or pos == 2) and not isCooker1Cooking and not isCooker2Cooking then
		PlaySFX("cook")
	end
	if pos == 1 then
		isCooker1Cooking = true
		SetCookerOn(GoCooker1,true)
		local foodBK = GoCooker1.transform:Find("Btn_Cook/Img_FoodBK").gameObject
		local food = GoCooker1.transform:Find("Btn_Cook/Img_Food").gameObject
		GoCooker1.transform:Find("Btn_Cook/Img_Empty").gameObject:SetActive(false)
		foodBK:SetActive(true)
		GoCooker1.transform:Find("Btn_Cook/Img_ProgressBG").gameObject:SetActive(true)
		food:SetActive(true)
		
		foodBK:GetComponent(typeof(CS.ExImage)).sprite = foodBGPicList[dishID-1]
		food:GetComponent(typeof(CS.ExImage)).sprite = foodPicList[dishID-1]
		
		Cooker1Holding = dishID
		cooker1TargetTime = RecipeInfo[dishID].finishTime
		UpdatePlayerSpineAnim()
		GOSmoke1:SetActive(true)
	end
	if pos == 2 then
		isCooker2Cooking = true
		SetCookerOn(GoCooker2,true)
		local foodBK = GoCooker2.transform:Find("Btn_Cook/Img_FoodBK").gameObject
		local food = GoCooker2.transform:Find("Btn_Cook/Img_Food").gameObject
		GoCooker2.transform:Find("Btn_Cook/Img_Empty").gameObject:SetActive(false)
		foodBK:SetActive(true)
		GoCooker2.transform:Find("Btn_Cook/Img_ProgressBG").gameObject:SetActive(true)
		food:SetActive(true)
		
		foodBK:GetComponent(typeof(CS.ExImage)).sprite = foodBGPicList[dishID-1]
		food:GetComponent(typeof(CS.ExImage)).sprite = foodPicList[dishID-1]
		
		Cooker2Holding = dishID
		cooker2TargetTime = RecipeInfo[dishID].finishTime
		UpdatePlayerSpineAnim()
		GOSmoke2:SetActive(true)
	end
end

function UpdateCookerLogic()
	if isCooker1Cooking then
		cooker1Timer = cooker1Timer + CS.UnityEngine.Time.deltaTime
		if cooker1Timer >= cooker1TargetTime then
			SetCookerOn(GoCooker1,false)
			isCooker1Cooking = false
			cooker1Timer = 0
			RefreshFoodPos()
			UpdatePlayerSpineAnim()
			PlaySFX("cookFinish")
			if not isCooker1Cooking and not isCooker2Cooking then
				PlaySFX("stopcook")
			end	
			GOSmoke1:SetActive(false)
		end
	end
	if isCooker2Cooking then
		cooker2Timer = cooker2Timer + CS.UnityEngine.Time.deltaTime
		if cooker2Timer >= cooker2TargetTime then
			SetCookerOn(GoCooker2,false)
			isCooker2Cooking = false
			cooker2Timer = 0
			RefreshFoodPos()
			UpdatePlayerSpineAnim()	
			PlaySFX("cookFinish")
			if not isCooker1Cooking and not isCooker2Cooking then
				PlaySFX("stopcook")
			end	
			GOSmoke2:SetActive(false)
		end
	end
	
	UpdateCookerUI()
end
local GoCooker1Pic2
local GoCooker1Pic3
local GoCooker2Pic2
local GoCooker2Pic3
function UpdateCookerUI()

	if isCooker1Cooking then

		if GoCooker1Pic2 == nil then
			GoCooker1Pic2 = GoCooker1.transform:Find("Btn_Cook/Img_ProgressBG").gameObject:GetComponent(typeof(CS.ExImage))
		end
		if GoCooker1Pic3 == nil then
			GoCooker1Pic3 = GoCooker1.transform:Find("Btn_Cook/Img_Food").gameObject:GetComponent(typeof(CS.ExImage))
		end
		local value = cooker1Timer/cooker1TargetTime
		GoCooker1Pic2.fillAmount = value
		GoCooker1Pic3.fillAmount = value
	end
	if isCooker2Cooking then
		if GoCooker2Pic2 == nil then
			GoCooker2Pic2 = GoCooker2.transform:Find("Btn_Cook/Img_ProgressBG").gameObject:GetComponent(typeof(CS.ExImage))
		end
		if GoCooker2Pic3 == nil then
			GoCooker2Pic3 = GoCooker2.transform:Find("Btn_Cook/Img_Food").gameObject:GetComponent(typeof(CS.ExImage))
		end
		local value = cooker2Timer/cooker2TargetTime
		GoCooker2Pic2.fillAmount = value
		GoCooker2Pic3.fillAmount = value
	end

end
function RefreshFoodPos()
	if foodPos1 == 0 then
		if Cooker1Holding ~= 0 and not isCooker1Cooking then
			foodPos1 = Cooker1Holding
			Cooker1Holding = 0
		else 
			if Cooker2Holding ~= 0 and not isCooker2Cooking  then
				foodPos1 = Cooker2Holding
				Cooker2Holding = 0
			end
		end
	end
	if foodPos2 == 0 then
		if Cooker1Holding ~= 0 and not isCooker1Cooking then
			foodPos2 = Cooker1Holding
			Cooker1Holding = 0
		else 
			if Cooker2Holding ~= 0  and not isCooker2Cooking then
				foodPos2 = Cooker2Holding
				Cooker2Holding = 0
			end
		end
	end
	if foodPos3 == 0 then
		if Cooker1Holding ~= 0 and not isCooker1Cooking then
			foodPos3 = Cooker1Holding
			Cooker1Holding = 0
		else 
			if Cooker2Holding ~= 0 and not isCooker2Cooking then
				foodPos3 = Cooker2Holding
				Cooker2Holding = 0
			end
		end
	end
	if OrderCustomer1 ~= nil then
		if HaveDish(OrderCustomer1.RequestingMenu) then
			GetOrderGO(1).transform:Find("Img_PreparedMask").gameObject:SetActive(true)
		else
			GetOrderGO(1).transform:Find("Img_PreparedMask").gameObject:SetActive(false)
		end
	end
	if OrderCustomer2 ~= nil then
		if HaveDish(OrderCustomer2.RequestingMenu) then
			GetOrderGO(2).transform:Find("Img_PreparedMask").gameObject:SetActive(true)
		else
			GetOrderGO(2).transform:Find("Img_PreparedMask").gameObject:SetActive(false)
		end
	end
	if OrderCustomer3 ~= nil then
		if HaveDish(OrderCustomer3.RequestingMenu) then
			GetOrderGO(3).transform:Find("Img_PreparedMask").gameObject:SetActive(true)
		else
			GetOrderGO(3).transform:Find("Img_PreparedMask").gameObject:SetActive(false)
		end
	end
	if OrderCustomer4 ~= nil then
		if HaveDish(OrderCustomer4.RequestingMenu) then
			GetOrderGO(4).transform:Find("Img_PreparedMask").gameObject:SetActive(true)
		else
			GetOrderGO(4).transform:Find("Img_PreparedMask").gameObject:SetActive(false)
		end
	end
	RefreshFoodPosUI()
end
function RefreshFoodPosUI()
	if foodPos1 == 0 then
		GoDish1:SetActive(false)
	else
		GoDish1:SetActive(true)
		GoDish1:GetComponent(typeof(CS.ExImage)).sprite = foodPicList[foodPos1-1]
		if IsTargetDishHaveBuff(foodPos1) then
			GoDish1.transform:GetChild(0).gameObject:GetComponent(typeof(CS.ExImage)).sprite = foodPicShineList[foodPos1-1]
			GoDish1.transform:GetChild(0).gameObject:SetActive(true)
		else
			GoDish1.transform:GetChild(0).gameObject:SetActive(false)
		end
	end
	if foodPos2 == 0 then
		GoDish2:SetActive(false)
	else
		GoDish2:SetActive(true)
		GoDish2:GetComponent(typeof(CS.ExImage)).sprite = foodPicList[foodPos2-1]
		if IsTargetDishHaveBuff(foodPos2) then
			GoDish2.transform:GetChild(0).gameObject:GetComponent(typeof(CS.ExImage)).sprite = foodPicShineList[foodPos2-1]
			GoDish2.transform:GetChild(0).gameObject:SetActive(true)
		else
			GoDish2.transform:GetChild(0).gameObject:SetActive(false)
		end
	end
	if foodPos3 == 0 then
		GoDish3:SetActive(false)
	else
		GoDish3:SetActive(true)
		GoDish3:GetComponent(typeof(CS.ExImage)).sprite = foodPicList[foodPos3-1]
		if IsTargetDishHaveBuff(foodPos3) then
			GoDish3.transform:GetChild(0).gameObject:GetComponent(typeof(CS.ExImage)).sprite = foodPicShineList[foodPos3-1]
			GoDish3.transform:GetChild(0).gameObject:SetActive(true)
		else
			GoDish3.transform:GetChild(0).gameObject:SetActive(false)
		end
	end
	if Cooker1Holding == 0 then
		local foodBK = GoCooker1.transform:Find("Btn_Cook/Img_FoodBK").gameObject
		local food = GoCooker1.transform:Find("Btn_Cook/Img_Food").gameObject
		GoCooker1.transform:Find("Btn_Cook/Img_Empty").gameObject:SetActive(true)
		GoCooker1.transform:Find("Btn_Cook/Img_CompletedBG").gameObject:SetActive(false)
		foodBK:SetActive(false)
		GoCooker1.transform:Find("Btn_Cook/Img_ProgressBG").gameObject:SetActive(false)
		food:SetActive(false)
	end
	if Cooker2Holding == 0 then
		local foodBK = GoCooker2.transform:Find("Btn_Cook/Img_FoodBK").gameObject
		local food = GoCooker2.transform:Find("Btn_Cook/Img_Food").gameObject
		GoCooker2.transform:Find("Btn_Cook/Img_Empty").gameObject:SetActive(true)
		GoCooker2.transform:Find("Btn_Cook/Img_CompletedBG").gameObject:SetActive(false)
		foodBK:SetActive(false)
		GoCooker2.transform:Find("Btn_Cook/Img_ProgressBG").gameObject:SetActive(false)
		food:SetActive(false)
	end
	if Cooker1Holding ~= 0 and not isCooker1Cooking then
		GoCooker1.transform:Find("Btn_Cook/Img_CompletedBG").gameObject:SetActive(true)
		GoCooker1.transform:Find("Btn_Cook/Img_ProgressBG").gameObject:SetActive(false)
	end
	if Cooker2Holding ~= 0 and not isCooker2Cooking then
		GoCooker2.transform:Find("Btn_Cook/Img_CompletedBG").gameObject:SetActive(true)
		GoCooker2.transform:Find("Btn_Cook/Img_ProgressBG").gameObject:SetActive(false)
	end
end
------------------Recipe相关--------------------
local RecipeWaitCloseTimer = 0
local RecipeWaitClose = false
local curIngredientInCook = {false,false,false,false,false,false}
function OpenRecipe()
	if not isRecipeOpen and not isPausing then
		GoRecipe:SetActive(true)
		PlaySFX("openUI")
		InitRecipePage()
	end
end
function UpdateRecipeWaitClose()

	if RecipeWaitClose then
		RecipeWaitCloseTimer = RecipeWaitCloseTimer + CS.UnityEngine.Time.deltaTime
		if RecipeWaitCloseTimer >= 0.75 then
			CloseRecipePage()
		end
	end
end
function InitRecipePage()
	isRecipeOpen = true
	--开启此界面时暂停游戏
	isPausing = true
	--检查现有食材
	for i=1,#RecipeInfo do
		GoRecipeLeftList.transform:GetChild(i-1):Find("On").gameObject:SetActive(RecipeInfo[i].isEnable)
		local goRemarks = {}
		for j = 1,4 do
			local goRemark = GoRecipeLeftList.transform:GetChild(i-1):Find("Remark"):GetChild(j-1).gameObject
			goRemarks[#goRemarks + 1] = goRemark
		end
		for j = 1,4 do
			local t = CheckDishRequesting(RecipeInfo[i].id,j)
			local goRemark = goRemarks[j]
			if t >= 0 and t <= 2 then
				goRemark:SetActive(true)
				if t == 2 then
					goRemark:GetComponent(typeof(CS.ExImage)).sprite = remarkPicList[0]
					goRemark.transform:SetAsFirstSibling()
				end
				if t == 1 then
					goRemark:GetComponent(typeof(CS.ExImage)).sprite = remarkPicList[1]
				end
				if t == 0 then
					goRemark:GetComponent(typeof(CS.ExImage)).sprite = remarkPicList[2]
					goRemark.transform:SetAsLastSibling()
				end
			else
				goRemark:SetActive(false)
			end
		end

		
	end
	curIngredientInCook = {false,false,false,false,false,false}
	--pan animation
	local goPan = GoRecipe.transform:Find("Main/Pan/Img_Pan")
	local goPanShadow = GoRecipe.transform:Find("Main/Pan/Img_Shadow")
	goPan.eulerAngles = CS.UnityEngine.Vector3(0,0,-90)
	goPan:DOLocalRotate(CS.UnityEngine.Vector3(0,0,0),0.4):SetDelay(0.1):Play()
	goPanShadow.eulerAngles = CS.UnityEngine.Vector3(0,0,-90)
	goPanShadow:DOLocalRotate(CS.UnityEngine.Vector3(0,0,0),0.4):SetDelay(0.1):Play()
	CheckCookDish()
	UpdateIngredientShowing()
	UpdateIngredientCookingUI()
end
function CheckDishRequesting(dishid,member)
	local level = -1
	if member == 1 and OrderCustomer1 ~= nil then
		if OrderCustomer1.RequestingMenu == dishid then
			if level < 0 then
				level = OrderCustomer1.patienceLevel
			else
				if OrderCustomer1.patienceLevel < level then
					level = OrderCustomer1.patienceLevel
				end
			end
		end
	end
	
	if member == 2 and OrderCustomer2 ~= nil then
		if OrderCustomer2.RequestingMenu == dishid then
			if level < 0 then
				level = OrderCustomer2.patienceLevel
			else
				if OrderCustomer2.patienceLevel < level then
					level = OrderCustomer2.patienceLevel
				end
			end
		end
	end
	
	if member == 3 and OrderCustomer3 ~= nil then
		if OrderCustomer3.RequestingMenu == dishid then
			if level < 0 then
				level = OrderCustomer3.patienceLevel
			else
				if OrderCustomer3.patienceLevel < level then
					level = OrderCustomer3.patienceLevel
				end
			end
		end	
	end
	
	if member == 4 and OrderCustomer4 ~= nil then
		if OrderCustomer4.RequestingMenu == dishid then
			if level < 0 then
				level = OrderCustomer4.patienceLevel
			else
				if OrderCustomer4.patienceLevel < level then
					level = OrderCustomer4.patienceLevel
				end
			end
		end
	end
		return level
end
function PutIngredient(id)
	local curIngredientCnt = 0
	for i=1,#curIngredientInCook do
		if curIngredientInCook[i] then
			curIngredientCnt = curIngredientCnt + 1
		end
	end
	if curIngredientCnt >= 4 and not curIngredientInCook[id]  then
		CS.CommonController.LightMessageTips(GetName(60152))
		return
	end
	curIngredientInCook[id] = not curIngredientInCook[id]
	if curIngredientInCook[id] then
		curIngredientCnt = curIngredientCnt + 1
	else
		curIngredientCnt = curIngredientCnt - 1
	end
	--print(curIngredientCnt)
	UpdateIngredientShowing(curIngredientCnt)
	CheckCookDish()
end
function UpdateIngredientShowing(curIngredientCnt)
	local ShowingPos = 1
	GoRecipeIngredient1:SetActive(false)
	GoRecipeIngredient2:SetActive(false)
	GoRecipeIngredient3:SetActive(false)
	GoRecipeIngredient4:SetActive(false)
	
	for i=1,#curIngredientInCook do
		if curIngredientInCook[i] then
			SetRecipeIngredientSprite(ShowingPos,i)
			ShowingPos = ShowingPos + 1
		end
	end
	GoRecipeIngredientE:SetActive(ShowingPos == 1)
	if curIngredientCnt == 1 then
		GoRecipe.transform:Find("Main/Pan/Timeline/Ingredients1").gameObject:GetComponent(typeof(CS.UnityEngine.Playables.PlayableDirector)):Play()
	end
	if curIngredientCnt == 2 then
		GoRecipe.transform:Find("Main/Pan/Timeline/Ingredients2").gameObject:GetComponent(typeof(CS.UnityEngine.Playables.PlayableDirector)):Play()
	end
	if curIngredientCnt == 3 then
		GoRecipe.transform:Find("Main/Pan/Timeline/Ingredients3").gameObject:GetComponent(typeof(CS.UnityEngine.Playables.PlayableDirector)):Play()
	end
	if curIngredientCnt == 4 then
		GoRecipe.transform:Find("Main/Pan/Timeline/Ingredients4").gameObject:GetComponent(typeof(CS.UnityEngine.Playables.PlayableDirector)):Play()
	end
end
function SetRecipeIngredientSprite(pos,type)
	local sprite = GoRecipe:GetComponent(typeof(CS.UGUISpriteHolder)).listSprite[type-1]
	if pos == 1 then
		GoRecipeIngredient1:SetActive(true)
		GoRecipeIngredient1.transform:GetChild(0).gameObject:GetComponent(typeof(CS.ExImage)).sprite = sprite
	end
	if pos == 2 then
		GoRecipeIngredient2:SetActive(true)
		GoRecipeIngredient2.transform:GetChild(0).gameObject:GetComponent(typeof(CS.ExImage)).sprite = sprite
	end
	if pos == 3 then
		GoRecipeIngredient3:SetActive(true)
		GoRecipeIngredient3.transform:GetChild(0).gameObject:GetComponent(typeof(CS.ExImage)).sprite = sprite
	end
	if pos == 4 then
		GoRecipeIngredient4:SetActive(true)
		GoRecipeIngredient4.transform:GetChild(0).gameObject:GetComponent(typeof(CS.ExImage)).sprite = sprite
	end
end
--检查目前放入的菜品 是否符合某一食谱的要求(需要完全一样)
local canCookDishNum = 0
local cancookFlag = false
function CheckCookDish()
	local canCook = false
	local currentIngredientNumber = 0
	for i=1,#curIngredientInCook do
		if curIngredientInCook[i] then
			currentIngredientNumber = currentIngredientNumber + 1
		end
	end
	for i=1,#RecipeInfo do
		if RecipeInfo[i].isEnable then
			local info = RecipeInfo[i].requireIngredient
			local flag = true
			for j = 1,#info do
				if not curIngredientInCook[info[j]] then
					flag = false
					break
				end			
			end
			if flag then
				if #info == currentIngredientNumber then
					canCook = true		
					canCookDishNum = i
					break
				end
			end
		end
		
	end
	cancookFlag = canCook
	if canCook then
		btnRecipeOK.interactable = true
	else
		btnRecipeOK.interactable = true
	end
	
end
function ClearCookDish()
	for i=1,#curIngredientInCook do
		if curIngredientInCook[i] then
			curIngredientInCook[i] = false
		end
	end
	UpdateIngredientShowing()
	CheckCookDish()
end
function EnsureCookDish()
	if isUIPausing then return end
	if not cancookFlag then
		CS.CommonController.LightMessageTips(GetName(60151))
		return 
	end
	for i=1,#curIngredientInCook do
		if curIngredientInCook[i] then
			IngredientInfo[i].isReady = false
			if IngredientInfo[i].haveExtra then
				IngredientInfo[i].haveExtra = false
				IngredientInfo[i].isReady = true
			end
		end	
	end
	ResumeIngredientCookingUI()
	CookDish(currentSelectCooker,canCookDishNum)
	GoRecipe.transform:Find("Main/Pan/Timeline/Pan").gameObject:GetComponent(typeof(CS.UnityEngine.Playables.PlayableDirector)):Play()
	RecipeWaitCloseTimer = 0
	RecipeWaitClose = true

end
function CloseRecipePage()
	if isUIPausing then return end
	if isRecipeOpen == false then return end
	isRecipeOpen = false
	isPausing = false
	RecipeWaitCloseTimer = 0
	RecipeWaitClose = false
	GoRecipe.transform:Find("Main").gameObject:GetComponents(typeof(CS.TweenPlay))[1].EndHandle = function()
		GoRecipe:SetActive(false)
	end
	GoRecipe.transform:Find("Main").gameObject:GetComponents(typeof(CS.TweenPlay))[1]:DoTween()
	UpdateIngredientCookingUI()
end

	
------------------Customer相关--------------------
local patienceGap = 10
local lvl1CustomerCnt = 0
local lvl2CustomerCnt = 0
local lvl3CustomerCnt = 0
local FailedCustomerCnt = 0
function InitCustomer()
	GetOrderGO(1).transform:Find("Btn_TouchArea").gameObject:GetComponent(typeof(CS.ExButton)).onClick:AddListener(function()					
			OnSelectOrder(1)
		end)
	GetOrderGO(2).transform:Find("Btn_TouchArea").gameObject:GetComponent(typeof(CS.ExButton)).onClick:AddListener(function()					
			OnSelectOrder(2)
		end)
	GetOrderGO(3).transform:Find("Btn_TouchArea").gameObject:GetComponent(typeof(CS.ExButton)).onClick:AddListener(function()					
			OnSelectOrder(3)
		end)
	GetOrderGO(4).transform:Find("Btn_TouchArea").gameObject:GetComponent(typeof(CS.ExButton)).onClick:AddListener(function()					
			OnSelectOrder(4)
		end)
end
function GenCustomerSpine(code,pos)
	local spine = CS.UnityEngine.Object.Instantiate(CS.CommonController.GetSpinePrefab("R_"..code))
	
	spine.transform:SetParent(GoSpineHolderCustomer.transform,false)
	spine:SetActive(true)
	spine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, "move", true, 0)
	spine:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = 16
	if pos <= 2 then
		spine.transform.localPosition = CustomerLeft
		spine.transform.localScale = CS.UnityEngine.Vector3(170,170,170)
	else
		spine.transform.localPosition = CustomerRight
		spine.transform.localScale = CS.UnityEngine.Vector3(-170,170,170)
	end
	if pos == 1 then
		CustomerSpine1 = spine
		spine.transform:DOLocalMove(CustomerPos1,2.4):OnComplete(function()
			spine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, "sit", true, 0)
			spine.transform:DOLocalMoveY(-30,0.06)
			spine:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = 15
		end):Play()
	end
	if pos == 2 then
		CustomerSpine2 = spine
		spine.transform:DOLocalMove(CustomerPos2,2.4):OnComplete(function()
				spine.transform.localScale = CS.UnityEngine.Vector3(-170,170,170)
				spine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, "sit", true, 0)
				spine.transform:DOLocalMoveY(-30,0.06)
				spine:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = 15
			end):Play()
	end
	if pos == 3 then
		CustomerSpine3 = spine
		spine.transform:DOLocalMove(CustomerPos3,2.4):OnComplete(function()
				spine.transform.localScale = CS.UnityEngine.Vector3(170,170,170)
				spine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, "sit", true, 0)
				spine.transform:DOLocalMoveY(-30,0.06)
				spine:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = 15
			end):Play()
	end
	if pos == 4 then
		CustomerSpine4 = spine
		spine.transform:DOLocalMove(CustomerPos4,2.4):OnComplete(function()
				spine:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, "sit", true, 0)
				spine.transform:DOLocalMoveY(-30,0.06)
				spine:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = 15
			end):Play()
	end
end
--刷新耐心条
function InitOrderUI(pos)
	local orderObj
	local orderCustomer
	if pos == 1 then
		orderObj = GetOrderGO(1)
		orderCustomer = OrderCustomer1
	end
	if pos == 2 then
		orderObj = GetOrderGO(2)
		orderCustomer = OrderCustomer2
	end
	if pos == 3 then
		orderObj = GetOrderGO(3)
		orderCustomer = OrderCustomer3
	end
	if pos == 4 then
		orderObj = GetOrderGO(4)
		orderCustomer = OrderCustomer4
	end
	--计算需要的中段
	local timeTotal = math.modf(orderCustomer.requireTime / 5)
	--删去或者添加中段
	local PatienceBG = orderObj.transform:Find("PatienceBG")
	local PatienceGO = orderObj.transform:Find("Patience")
	local PatienceBGMid = orderObj.transform:Find("PatienceBG/Img_Middle")
	local PatienceGOMid = orderObj.transform:Find("Patience/Img_Middle")
	local PatienceBGEnd = orderObj.transform:Find("PatienceBG/Img_Bottom")
	local PatienceGOEnd = orderObj.transform:Find("Patience/Img_Bottom")
	local curTotal = PatienceBG:GetChildCount() - 1
	if curTotal  > timeTotal then
		local cnt = curTotal - timeTotal
		for i = 3, 3+cnt-1 do
			CS.UnityEngine.Object.Destroy(PatienceBG:GetChild(i).gameObject)
			CS.UnityEngine.Object.Destroy(PatienceGO:GetChild(i).gameObject)
		end
	else
		if curTotal  < timeTotal  then
			local cnt = timeTotal - curTotal
			for i = 1, cnt do
				CS.UnityEngine.Object.Instantiate(PatienceBGMid.gameObject,PatienceBG,false)
				CS.UnityEngine.Object.Instantiate(PatienceGOMid.gameObject,PatienceGO,false)
			end
			PatienceBGEnd:SetAsLastSibling()
			PatienceGOEnd:SetAsLastSibling()
		end
	end
	--染色 等1帧让销毁进行
	PatienceGO.transform:DOLocalMove(PatienceGO.transform.localPosition,0.01):OnComplete(
		function()					
			OrderUIPaint(pos)
		end)
end

function OrderUIPaint(pos)
	local orderObj
	local orderCustomer
	if pos == 1 then
		orderObj = GetOrderGO(1)
		orderCustomer = OrderCustomer1
	end
	if pos == 2 then
		orderObj = GetOrderGO(2)
		orderCustomer = OrderCustomer2
	end
	if pos == 3 then
		orderObj = GetOrderGO(3)
		orderCustomer = OrderCustomer3
	end
	if pos == 4 then
		orderObj = GetOrderGO(4)
		orderCustomer = OrderCustomer4
	end
	local patienceCnt = 0
	local PatienceGO = orderObj.transform:Find("Patience")
	for i = 1,PatienceGO:GetChildCount()-1 do
		patienceCnt = patienceCnt + 5
		if patienceCnt <= orderCustomer.guestInfo.patience1 then
			PatienceGO:GetChild(i):GetChild(0).gameObject:GetComponent(typeof(CS.ExImage)).color = GenColor(189,254,34,255)
		else
			if patienceCnt <= (orderCustomer.guestInfo.patience1 + orderCustomer.guestInfo.patience2) then
				PatienceGO:GetChild(i):GetChild(0).gameObject:GetComponent(typeof(CS.ExImage)).color = GenColor(254,196,34,255)
			else
				PatienceGO:GetChild(i):GetChild(0).gameObject:GetComponent(typeof(CS.ExImage)).color = GenColor(254,34,74,255)
			end
		end
	end
end
function RecoverCustomerPatience(value)
	for i=1, #stageGuestList do
		if stageGuestList[i].isRequesting then
			stageGuestList[i].timer = stageGuestList[i].timer - value
			if stageGuestList[i].timer < 0 then
				stageGuestList[i].timer = 0
			end
		end
	end
end
function UpdateCustomer()
	for i=1, #stageGuestList do
		if stageGuestList[i].isRequesting then
			stageGuestList[i].timer = stageGuestList[i].timer + CS.UnityEngine.Time.deltaTime
			if stageGuestList[i].timer >= stageGuestList[i].requireTime then
				ResetCustomer(i,true)
			end
		end
	end
	UpdateOrderUI()
end	
function UpdateOrderUI()
	if OrderCustomer1 ~= nil then
		UpdateOrderPos(OrderCustomer1,GetOrderGO(1),1)		
	end
	
	if OrderCustomer2 ~= nil then
		UpdateOrderPos(OrderCustomer2,GetOrderGO(2),2)		
	end
	
	if OrderCustomer3 ~= nil then
		UpdateOrderPos(OrderCustomer3,GetOrderGO(3),3)		
	end
	
	if OrderCustomer4 ~= nil then
		UpdateOrderPos(OrderCustomer4,GetOrderGO(4),4)		
	end
end
function UpdateOrderPos(customer,GoOrder,pos)
	if customer.timer >= 0 then
		if customer.patienceLevel > 2 then
			customer.patienceLevel = 2
			RefreshOrderUI(pos)
		end
	end
	if customer.patienceLevel <= 2 then
		GoOrder.transform:Find("Patience"):GetComponent(typeof(CS.ExImage)).fillAmount = 1 - (customer.timer / customer.requireTime)
	end
	if customer.timer >= customer.guestInfo.patience1 then
		if customer.patienceLevel > 1 then
			customer.patienceLevel = 1
			--GoOrder1.transform:Find("Img_Patience").gameObject:GetComponent(typeof(CS.ExImage)).sprite = PatiencePicList[1]
		end
	end
	if customer.timer >= customer.guestInfo.patience1 + customer.guestInfo.patience2 then
		if customer.patienceLevel > 0 then
			customer.patienceLevel = 0
			GoOrder.transform:Find("Img_Warning").gameObject:SetActive(true)
		end
	end
end
function ShowOrderUIEmojiAndScore(pos,isFail)
	local score
	local patience
	local code = ""
	local customer
	local goOrder
	if pos == 1 then
		if OrderCustomer1 ~= nil then
			customer = OrderCustomer1
			goOrder = GetOrderGO(1)
			order1WaitAnim = true
		end
	end
	if pos == 2 then
		if OrderCustomer2 ~= nil then
			customer = OrderCustomer2
			goOrder = GetOrderGO(2)
			order2WaitAnim = true
		end
	end
	if pos == 3 then
		if OrderCustomer3 ~= nil then
			customer = OrderCustomer3
			goOrder = GetOrderGO(3)
			order3WaitAnim = true
		end
	end
	if pos == 4 then
		if OrderCustomer4 ~= nil then
			customer = OrderCustomer4
			goOrder = GetOrderGO(4)
			order4WaitAnim = true
		end
	end
	if isFail then
		score = customerLeaveMinus
		local rnd = math.random(1,#emojiListFail)
		code = emojiListFail[rnd]
	else
		score = customer.finalScore
		patience = customer.patienceLevel
		if patience >= 2 then
			local rnd = math.random(1,#emojiListLv3)
			code = emojiListLv3[rnd]
		end
		if patience == 1 then
			local rnd = math.random(1,#emojiListLv2)
			code = emojiListLv2[rnd]
		end
		if patience == 0 then
			local rnd = math.random(1,#emojiListLv1)
			code = emojiListLv1[rnd]
		end		
	end	
	if(stageNum ~= 4) then	
		goOrder.transform:Find("EmojiBG").gameObject:SetActive(true)
		goOrder.transform:Find("EmojiBG/Img_Emoji").gameObject:GetComponent(typeof(CS.ExImage)).sprite = GetEmojiSprite(code)
		if not isFail then
			goOrder.transform:Find("Img_CookedFood").gameObject:SetActive(true)
		end
	end
	goOrder.transform:Find("Tex_Score").gameObject:SetActive(true)
	if score <= 0 then
		goOrder.transform:Find("Tex_Score").gameObject:GetComponent(typeof(CS.ExText)).text = tostring(score)
	else
		goOrder.transform:Find("Tex_Score").gameObject:GetComponent(typeof(CS.ExText)).text ='+'..tostring(score)
	end
end
function RefreshOrderUI(pos)
	if pos == 1 then
		if OrderCustomer1 ~= nil then
			GetOrderGO(1):SetActive(true)		
			GetOrderGO(1).transform:Find("Img_Warning").gameObject:SetActive(false)
			GetOrderGO(1).transform:Find("Img_OrderFood").gameObject:GetComponent(typeof(CS.ExImage)).sprite  = foodPicList[OrderCustomer1.RequestingMenu-1]
			GetOrderGO(1).transform:Find("Tex_Score").gameObject:SetActive(false)
			if HaveDish(OrderCustomer1.RequestingMenu) then
				GetOrderGO(1).transform:Find("Img_PreparedMask").gameObject:SetActive(true)
			else
				GetOrderGO(1).transform:Find("Img_PreparedMask").gameObject:SetActive(false)
			end
			if stageNum ~= 4 then
				GetOrderGO(1).transform:Find("EmojiBG").gameObject:SetActive(false)
				GetOrderGO(1).transform:Find("Img_CookedFood").gameObject:SetActive(false)
				GetOrderGO(1).transform:Find("Img_CookedFood").gameObject:GetComponent(typeof(CS.ExImage)).sprite  = foodPicList[OrderCustomer1.RequestingMenu-1]
			end
		else
			GetOrderGO(1):SetActive(false)
		end
	end
	if pos == 2 then
		if OrderCustomer2 ~= nil then
			GetOrderGO(2):SetActive(true)	
			GetOrderGO(2).transform:Find("Img_Warning").gameObject:SetActive(false)
			GetOrderGO(2).transform:Find("Img_OrderFood").gameObject:GetComponent(typeof(CS.ExImage)).sprite  = foodPicList[OrderCustomer2.RequestingMenu-1]
			GetOrderGO(2).transform:Find("Tex_Score").gameObject:SetActive(false)
			if HaveDish(OrderCustomer2.RequestingMenu) then
				GetOrderGO(2).transform:Find("Img_PreparedMask").gameObject:SetActive(true)
			else
				GetOrderGO(2).transform:Find("Img_PreparedMask").gameObject:SetActive(false)
			end
			if stageNum ~= 4 then
				GetOrderGO(2).transform:Find("EmojiBG").gameObject:SetActive(false)
				GetOrderGO(2).transform:Find("Img_CookedFood").gameObject:SetActive(false)
				GetOrderGO(2).transform:Find("Img_CookedFood").gameObject:GetComponent(typeof(CS.ExImage)).sprite  = foodPicList[OrderCustomer2.RequestingMenu-1]
			end
		else
			GetOrderGO(2):SetActive(false)
		end
	end
	if pos == 3 then
		if OrderCustomer3 ~= nil then
			GetOrderGO(3):SetActive(true)	
			GetOrderGO(3).transform:Find("Img_Warning").gameObject:SetActive(false)
			GetOrderGO(3).transform:Find("Img_OrderFood").gameObject:GetComponent(typeof(CS.ExImage)).sprite  = foodPicList[OrderCustomer3.RequestingMenu-1]	
			GetOrderGO(3).transform:Find("Tex_Score").gameObject:SetActive(false)
			if HaveDish(OrderCustomer3.RequestingMenu) then
				GetOrderGO(3).transform:Find("Img_PreparedMask").gameObject:SetActive(true)
			else
				GetOrderGO(3).transform:Find("Img_PreparedMask").gameObject:SetActive(false)
			end
			if stageNum ~= 4 then
				GetOrderGO(3).transform:Find("EmojiBG").gameObject:SetActive(false)
				GetOrderGO(3).transform:Find("Img_CookedFood").gameObject:SetActive(false)
				GetOrderGO(3).transform:Find("Img_CookedFood").gameObject:GetComponent(typeof(CS.ExImage)).sprite  = foodPicList[OrderCustomer3.RequestingMenu-1]
			end
		else
			GetOrderGO(3):SetActive(false)
		end
	end
	if pos == 4 then
		if OrderCustomer4 ~= nil then
			GetOrderGO(4):SetActive(true)
			GetOrderGO(4).transform:Find("Img_Warning").gameObject:SetActive(false)
			GetOrderGO(4).transform:Find("Img_OrderFood").gameObject:GetComponent(typeof(CS.ExImage)).sprite  = foodPicList[OrderCustomer4.RequestingMenu-1]		
			GetOrderGO(4).transform:Find("Tex_Score").gameObject:SetActive(false)
			if HaveDish(OrderCustomer4.RequestingMenu) then
				GetOrderGO(4).transform:Find("Img_PreparedMask").gameObject:SetActive(true)
			else
				GetOrderGO(4).transform:Find("Img_PreparedMask").gameObject:SetActive(false)
			end
			if stageNum ~= 4 then
				GetOrderGO(4).transform:Find("EmojiBG").gameObject:SetActive(false)
				GetOrderGO(4).transform:Find("Img_CookedFood").gameObject:SetActive(false)
				GetOrderGO(4).transform:Find("Img_CookedFood").gameObject:GetComponent(typeof(CS.ExImage)).sprite  = foodPicList[OrderCustomer4.RequestingMenu-1]
			end
		else
			GetOrderGO(4):SetActive(false)
		end
	end
end

function ResetCustomer(id,isFail)
	
	--print("ResetCustomer"..id)
	if isFail then
		FailedCustomerCnt = FailedCustomerCnt + 1 
		PlaySFX("customerLeave")
		SetScore(customerLeaveMinus)
	else
		if stageGuestList[id].patienceLevel >= 2 then
			lvl3CustomerCnt = lvl3CustomerCnt + 1
		end
		if stageGuestList[id].patienceLevel == 1 then
			lvl2CustomerCnt = lvl2CustomerCnt + 1
		end
		if stageGuestList[id].patienceLevel == 0 then
			lvl1CustomerCnt = lvl1CustomerCnt + 1
		end
		PlaySFX("customerFinish")
	end

	stageGuestList[id].timer = 0
	stageGuestList[id].isRequesting = false
	if OrderCustomer1 == stageGuestList[id] then
		ShowOrderUIEmojiAndScore(1,isFail)
		OrderCustomer1 = nil
		CustomerSpineLeave(CustomerSpine1,1)
		--CustomerSpine1 = nil
		if stageNum == 4 then
			RefreshOrderUI(1)		
		end	
	end
	if OrderCustomer2 == stageGuestList[id] then
		ShowOrderUIEmojiAndScore(2,isFail)
		OrderCustomer2 = nil
		CustomerSpineLeave(CustomerSpine2,2)
		CustomerSpine2 = nil
		if stageNum == 4 then
			RefreshOrderUI(2)		
		end		
	end
	if OrderCustomer3 == stageGuestList[id] then
		ShowOrderUIEmojiAndScore(3,isFail)
		OrderCustomer3 = nil	
		CustomerSpineLeave(CustomerSpine3,3)
		CustomerSpine3 = nil
		if stageNum == 4 then
			RefreshOrderUI(3)		
		end				
	end
	if OrderCustomer4 == stageGuestList[id] then
		ShowOrderUIEmojiAndScore(4,isFail)
		OrderCustomer4 = nil	
		CustomerSpineLeave(CustomerSpine4,4)
		CustomerSpine4 = nil
		if stageNum == 4 then
			RefreshOrderUI(4)		
		end				
	end	
end
function CustomerSpineLeave(spine,pos)
	local spineObj
	if spine == nil then
		if pos == 1 then order1WaitAnim = false end
		if pos == 2 then order2WaitAnim = false end
		if pos == 3 then order3WaitAnim = false end
		if pos == 4 then order4WaitAnim = false end
		return 
	else
		spineObj = spine.gameObject
	end
	local downpos = CustomerPos1
	if pos == 2 then
		downpos = CustomerPos2
	end
	if pos == 3 then
		downpos = CustomerPos3
	end
	if pos == 4 then
		downpos = CustomerPos4
	end
	
	spineObj.transform:DOLocalMoveY(-30,0.06):SetDelay(1.5):OnComplete(function()
			RefreshOrderUI(pos)
			spineObj:GetComponent(typeof(CS.SkeletonAnimation)).state:AddAnimation(0, "move", true, 0)
			spineObj.transform:DOLocalMove(downpos,0.1):OnComplete(function()
					spineObj:GetComponent(typeof(CS.UnityEngine.Renderer)).sortingOrder = 16
					if pos <= 2 then
						spineObj.transform.localScale = CS.UnityEngine.Vector3(-170,170,170)
						spineObj.transform:DOLocalMove(CustomerLeft,1.85):OnComplete(function()
								CS.UnityEngine.Object.Destroy(spineObj)
								if pos == 1 then order1WaitAnim = false end
								if pos == 2 then order2WaitAnim = false end
								if pos == 3 then order3WaitAnim = false end
								if pos == 4 then order4WaitAnim = false end
								
							end)
					else
						spineObj.transform.localScale = CS.UnityEngine.Vector3(170,170,170)
						spineObj.transform:DOLocalMove(CustomerRight,1.85):OnComplete(function()
								CS.UnityEngine.Object.Destroy(spineObj)
								if pos == 1 then order1WaitAnim = false end
								if pos == 2 then order2WaitAnim = false end
								if pos == 3 then order3WaitAnim = false end
								if pos == 4 then order4WaitAnim = false end
							end)
					end
				end)
		end):Play()
	
	

end
function ClearAllOrder()
	if OrderCustomer1 ~= nil then
		OrderCustomer1.timer = 0
		OrderCustomer1.isRequesting = false
		OrderCustomer1 = nil
		if CustomerSpine1 ~= nil then
			CS.UnityEngine.Object.Destroy(CustomerSpine1.gameObject)
		end
		CustomerSpine1 = nil
		RefreshOrderUI(1)			
	end
	if OrderCustomer2 ~= nil then
		OrderCustomer2.timer = 0
		OrderCustomer2.isRequesting = false
		OrderCustomer2 = nil
		if CustomerSpine2 ~= nil then
			CS.UnityEngine.Object.Destroy(CustomerSpine2.gameObject)
		end
		CustomerSpine2 = nil
		RefreshOrderUI(2)			
	end
	if OrderCustomer3 ~= nil then
		OrderCustomer3.timer = 0
		OrderCustomer3.isRequesting = false
		OrderCustomer3 = nil
		if CustomerSpine3 ~= nil then
			CS.UnityEngine.Object.Destroy(CustomerSpine3.gameObject)
		end
		CustomerSpine3 = nil
		RefreshOrderUI(3)			
	end
	if OrderCustomer4 ~= nil then
		OrderCustomer4.timer = 0
		OrderCustomer4.isRequesting = false
		OrderCustomer4 = nil
		if CustomerSpine4 ~= nil then
			CS.UnityEngine.Object.Destroy(CustomerSpine4.gameObject)
		end
		CustomerSpine4 = nil
		RefreshOrderUI(4)			
	end	
end
function OnSelectOrder(id)
	--print("OnSelectOrder"..id)
	if id == 1 then
		if OrderCustomer1 ~= nil then
			if FinishOrderDish(OrderCustomer1.RequestingMenu,OrderCustomer1.id) then
				ResetCustomer(OrderCustomer1.id,false)
			else
				OnSelectCooker(-1)
			end
		end	
	end
	if id == 2 then
		if OrderCustomer2 ~= nil then
			if FinishOrderDish(OrderCustomer2.RequestingMenu,OrderCustomer2.id) then
				ResetCustomer(OrderCustomer2.id,false)
			else
				OnSelectCooker(-1)
			end
		end	
	end
	if id == 3 then
		if OrderCustomer3 ~= nil then
			if FinishOrderDish(OrderCustomer3.RequestingMenu,OrderCustomer3.id) then
				ResetCustomer(OrderCustomer3.id,false)
			else
				OnSelectCooker(-1)
			end
		end	
	end
	if id == 4 then
		if OrderCustomer4 ~= nil then
			if FinishOrderDish(OrderCustomer4.RequestingMenu,OrderCustomer4.id) then
				ResetCustomer(OrderCustomer4.id,false)
			else
				OnSelectCooker(-1)
			end
		end	
	end
end
function FinishOrderDish(dishid,Customerid)
	--print("FinishOrderDish"..dishid..' '..foodPos1..' '..foodPos2..' '..foodPos3..' '..Cooker1Holding..' '..Cooker2Holding)
	local flag = false
	flag = RemoveDish(dishid)
	if flag then
		--得分		
		CalcScore(dishid,Customerid)
	end

	return flag
end
------------------得分判断相关--------------------

local dishScoreMultiplyList1 = {}
local dishScoreMultiplyList2 = {}
local dishScoreMultiplyList3 = {}
local dishScoreMultiplyList4 = {}
local dishScoreMultiplyList5 = {}
local dishScoreFixedList1 = {}
local dishScoreFixedList2 = {}
local dishScoreFixedList3 = {}
local dishScoreFixedList4 = {}
local dishScoreFixedList5 = {}
local anyScoreMultiplyList = {}
--分菜品的得分乘区
local dishScoreMultiply = 0
--分菜品的得分增加
local dishScoreFixed = 0
--任意菜品的得分乘区
local anyScoreMultiply = 0
local scorelvl1 = 0.25
local scorelvl2 = 0.5
local scorelvl3 = 1.0


function InitScoreTable()
	TableStruct = {}
end
function CalcScore(dishid,customerid)
	local baseScore = RecipeInfo[dishid].score +customerPatienceBonus[stageGuestList[customerid].patienceLevel + 1] + GetTargetDishScoreFixed(dishid)
	GetAnyScoreMultiply()
	GetTargetDishScoreMultiply(dishid)
	local score = math.floor(baseScore * (1+dishScoreMultiply+anyScoreMultiply))
	--print("CalcScore "..baseScore..' '..dishScoreMultiply..' '..anyScoreMultiply..' '..score)
	SetScore(score)
	stageGuestList[customerid].finalScore = score
	RefreshFoodPosUI()
end
function AddAnyScoreMultiply(arg,count)
	TableStruct = {level = arg, cnt = count}
	local flag = true
	for i = 1,#anyScoreMultiplyList do
		if anyScoreMultiplyList[i].cnt <= 0 then
			anyScoreMultiplyList[i] = TableStruct
			flag = false
			break
		end		
	end
	if flag then
		anyScoreMultiplyList[#anyScoreMultiplyList + 1] = TableStruct
	end
end
function GetValueByLvl(lvl)
	if lvl == 1 then
		return scorelvl1
	end
	if lvl == 2 then
		return scorelvl2
	end
	if lvl == 3 then
		return scorelvl3
	end
end
function GetAnyScoreMultiply()
	anyScoreMultiply = 0
	if #anyScoreMultiplyList > 0 then
		for i = 1,#anyScoreMultiplyList do
			if anyScoreMultiplyList[i].cnt > 0 then
				anyScoreMultiply = anyScoreMultiply + GetValueByLvl(anyScoreMultiplyList[i].level)
				anyScoreMultiplyList[i].cnt = anyScoreMultiplyList[i].cnt -1
			end		
		end
	end
end
function IsTargetDishHaveBuff(dish)
	local dishScoreFixedList = dishScoreFixedList1
	local dishScoreMultiplyList = dishScoreMultiplyList1
	if dish == 2 then
		dishScoreFixedList = dishScoreFixedList2
		dishScoreMultiplyList = dishScoreMultiplyList2
	end
	if dish == 3 then
		dishScoreFixedList = dishScoreFixedList3
		dishScoreMultiplyList = dishScoreMultiplyList3
	end
	if dish == 4 then
		dishScoreFixedList = dishScoreFixedList4
		dishScoreMultiplyList = dishScoreMultiplyList4
	end
	if dish == 5 then
		dishScoreFixedList = dishScoreFixedList5
		dishScoreMultiplyList = dishScoreMultiplyList5
	end
	for i = 1,#dishScoreFixedList do
		if dishScoreFixedList[i].cnt > 0 then
			--print("IsTargetDishHaveBuffFixed"..' '..dish..' '..#dishScoreFixedList..' '..i..' '..dishScoreFixedList[i].cnt)
			return true
		end		
	end	
	for i = 1,#dishScoreMultiplyList do
		if dishScoreMultiplyList[i].cnt > 0 then
			--print("IsTargetDishHaveBuffMultiply"..' '..dish..' '..#dishScoreMultiplyList..' '..i..' '..dishScoreMultiplyList[i].cnt)
			return true
		end		
	end
	return false
end
function AddTargetDishScoreFixed(dish,arg,count)
	local dishScoreFixedList = dishScoreFixedList1
	if dish == 2 then
		dishScoreFixedList = dishScoreFixedList2
	end
	if dish == 3 then
		dishScoreFixedList = dishScoreFixedList3
	end
	if dish == 4 then
		dishScoreFixedList = dishScoreFixedList4
	end
	if dish == 5 then
		dishScoreFixedList = dishScoreFixedList5
	end
	TableStruct = {change = arg, cnt = count}
	local flag = true
	for i = 1,#dishScoreFixedList do
		if dishScoreFixedList[i].cnt <= 0 then
			dishScoreFixedList[i] = TableStruct
			flag = false
			break
		end		
	end
	if flag then
		dishScoreFixedList[#dishScoreFixedList + 1] = TableStruct
	end
	RefreshFoodPosUI()
end
function AddTargetDishScoreMultiply(dish,arg,count)
	local dishScoreMultiplyList = dishScoreMultiplyList1
	if dish == 2 then
		dishScoreMultiplyList = dishScoreMultiplyList2
	end
	if dish == 3 then
		dishScoreMultiplyList = dishScoreMultiplyList3
	end
	if dish == 4 then
		dishScoreMultiplyList = dishScoreMultiplyList4
	end
	if dish == 5 then
		dishScoreMultiplyList = dishScoreMultiplyList5
	end
	TableStruct = {level = arg, cnt = count}
	local flag = true
	for i = 1,#dishScoreMultiplyList do
		if dishScoreMultiplyList[i].cnt <= 0 then
			dishScoreMultiplyList[i] = TableStruct
			flag = false
			break
		end		
	end
	if flag then
		dishScoreMultiplyList[#dishScoreMultiplyList + 1] = TableStruct
	end
	RefreshFoodPosUI()
end
function GetTargetDishScoreFixed(dishid)
	local dishScoreFixedList = dishScoreFixedList1
	if dishid == 2 then
		dishScoreFixedList = dishScoreFixedList2
	end
	if dishid == 3 then
		dishScoreFixedList = dishScoreFixedList3
	end
	if dishid == 4 then
		dishScoreFixedList = dishScoreFixedList4
	end
	if dishid == 5 then
		dishScoreFixedList = dishScoreFixedList5
	end
	dishScoreFixed = 0
	if #dishScoreFixedList > 0 then
		for i = 1,#dishScoreFixedList do
			if dishScoreFixedList[i].cnt > 0 then
				dishScoreFixed = dishScoreFixed + dishScoreFixedList[i].change
				dishScoreFixedList[i].cnt = dishScoreFixedList[i].cnt - 1
			end		
		end
	end
	return dishScoreFixed
end
function GetTargetDishScoreMultiply(dishid)
	local dishScoreMultiplyList = dishScoreMultiplyList1
	if dishid == 2 then
		dishScoreMultiplyList = dishScoreMultiplyList2
	end
	if dishid == 3 then
		dishScoreMultiplyList = dishScoreMultiplyList3
	end
	if dishid == 4 then
		dishScoreMultiplyList = dishScoreMultiplyList4
	end
	if dishid == 5 then
		dishScoreMultiplyList = dishScoreMultiplyList5
	end
	dishScoreMultiply = 0
	if #dishScoreMultiplyList > 0 then
		for i = 1,#dishScoreMultiplyList do
			if dishScoreMultiplyList[i].cnt > 0 then
				dishScoreMultiply = dishScoreMultiply + GetValueByLvl(dishScoreMultiplyList[i].level)
				dishScoreMultiplyList[i].cnt = dishScoreMultiplyList[i].cnt - 1
			end		
		end
	end
	
end
function SetScore(score)
	currentScore = currentScore + score
	if currentScore < 0 then
		currentScore = 0
	end
	RefreshScoreUI()
	if stageNum ~= 5 and currentScore >= TargetScore then
		StartOpenResultPage()
	end
end

function SetTargetScore(score,init)
	if not init then
		TextScore.transform:GetChild(0).gameObject:GetComponent(typeof(CS.ExText)).text  = '+'..(score-TargetScore)
		TextScore.transform:GetChild(0).gameObject:SetActive(false)
		TextScore.transform:GetChild(0).gameObject:SetActive(true)
	end
	TargetScore = score
	
	RefreshScoreUI()
end
function RefreshScoreUI()
	local s = tostring(currentScore)
	--local zeronum = 6 - #s
	--local zerostr = ""
	--if zeronum > 0 then
	--	for i =1,zeronum do
	--		zerostr = zerostr .. '0'		
	--	end
	--end
	TextScore:GetComponent(typeof(CS.ExText)).text = s..'/'..TargetScore
	local percent = currentScore/TargetScore
	if percent > 1 then percent = 1 end
	ImageScorePercent:GetComponent(typeof(CS.ExImage)):DOFillAmount(percent,0.8 * percent)
	if stageNum ==  5 then
		local rank = GetEndlessRank()
		if rank ==  1 then
			ImageScorePercent:GetComponent(typeof(CS.ExImage)).color = GenColor(214,165,128,255)
		end
		if rank ==  2 then
			ImageScorePercent:GetComponent(typeof(CS.ExImage)).color = GenColor(37,127,238,255)
		end
		if rank ==  3 then
			ImageScorePercent:GetComponent(typeof(CS.ExImage)).color = GenColor(240,35,92,255)
		end
		if rank ==  4 then
			ImageScorePercent:GetComponent(typeof(CS.ExImage)).color = GenColor(255,180,0,255)
		end
		if rank ==  5 then
			ImageScorePercent:GetComponent(typeof(CS.ExImage)).color = GenColor(142,201,40,255)
		end
	end
	--TextTotalScore:GetComponent(typeof(CS.ExText)).text =  string.format("%06d",(TargetScore))
end
------------------事件系统相关--------------------
local EventInterval = 20
local EventTimer = 0
local eventRnd = 5
local EventWaitCloseTimer = 0
local EventWaitClose = false

local takeoutPos = {0,0,0,0,0}
local takeoutBtn = {nil,nil,nil,nil,nil}
local takeoutEventFinishCnt = 0
function InitEventPool()
	
	local cnt = 1
	for i=1, #EventInfoList do
		
		if EventInfoList[i].isInital and  stageNum >= EventInfoList[i].level then
			TableStruct = {id = cnt, info = EventInfoList[i], timer = 0, targetTime = EventInfoList[i].requireTime}
			EventPool[cnt] = TableStruct	
			cnt = cnt + 1		
		end
	end
	--print("InitEventPool"..cnt)
end
function RemoveEventFromEventPool(id)
	for i=1, #EventPool do
		if EventPool[i] ~= nil and EventPool[i].info.id == id then
			table.remove(EventPool,i)
			break
		end		
	end
end
function AddEventToEventPool(id)
	if id <= #EventInfoList then
		local event = EventInfoList[id]
		local cnt = #EventInfoList + 1
		TableStruct = {id = cnt, info = event, timer = 0, targetTime = event.requireTime}
		EventPool[cnt] = TableStruct	
	end
end
local eventAnimTimer = 1
function UpdateEvent()
	if currentEvent == nil then
		EventTimer = EventTimer + CS.UnityEngine.Time.deltaTime
		
		if EventTimer >= EventInterval then
			EventTimer = math.random(-eventRnd,eventRnd)
			GenEvent()			
		end
	else
		currentEvent.timer = currentEvent.timer + CS.UnityEngine.Time.deltaTime
		UpdateEventUI()
		if currentEvent.timer >= eventAnimTimer * 5 then
			eventAnimTimer = eventAnimTimer + 1
			GOEventHint:GetComponents(typeof(CS.TweenPlay))[1]:DoTween()
		end
		if currentEvent.timer >= currentEvent.info.eventTime then
			ResolveCurrentEvent(-1)
		end

	end
	
end
function UpdateEventWaitClose()
	if isEventOpen and EventWaitClose then
		EventWaitCloseTimer = EventWaitCloseTimer + CS.UnityEngine.Time.deltaTime
		if EventWaitCloseTimer >= 3 then
			CloseEventPage()
		end
	end
end
function GenEvent()

	if #EventPool > 0 then
		local rnd = math.random(1,#EventPool)
		currentEvent = EventPool[rnd]
		currentEvent.timer = 0
	--print("GenEvent"..#EventPool..rnd..tostring(currentEvent == nil))
		PlaySFX("newEvent")
		RefreshEventUI()
		eventAnimTimer = 1
	end
end
function RefreshEventUI()
	--print("RefreshEventUI"..tostring(currentEvent == nil))
	if currentEvent ~= nil then
		GOEventHint:SetActive(true)
		local orderObj = GOEventPatience
		--计算需要的中段
		local timeTotal = math.modf(currentEvent.info.eventTime / 5)
		--删去或者添加中段
		local PatienceBG = orderObj.transform:Find("PatienceBG")
		local PatienceGO = orderObj.transform:Find("Patience")
		local PatienceBGMid = orderObj.transform:Find("PatienceBG/Img_Middle")
		local PatienceGOMid = orderObj.transform:Find("Patience/Img_Middle")
		local PatienceBGEnd = orderObj.transform:Find("PatienceBG/Img_Bottom")
		local PatienceGOEnd = orderObj.transform:Find("Patience/Img_Bottom")
		PatienceBG.gameObject:SetActive(true)
		PatienceGO.gameObject:SetActive(true)
		local curTotal = PatienceBG:GetChildCount() - 1
		if curTotal  > timeTotal then
			local cnt = curTotal - timeTotal
			for i = 3, 3+cnt-1 do
				CS.UnityEngine.Object.Destroy(PatienceBG:GetChild(i).gameObject)
				CS.UnityEngine.Object.Destroy(PatienceGO:GetChild(i).gameObject)
			end
		else
			if curTotal  < timeTotal  then
				local cnt = timeTotal - curTotal
				for i = 1, cnt do
					CS.UnityEngine.Object.Instantiate(PatienceBGMid.gameObject,PatienceBG,false)
					CS.UnityEngine.Object.Instantiate(PatienceGOMid.gameObject,PatienceGO,false)
				end
				PatienceBGEnd:SetAsLastSibling()
				PatienceGOEnd:SetAsLastSibling()
			end
		end
		--染色 等1帧让销毁进行
		PatienceGO.transform:DOLocalMove(PatienceGO.transform.localPosition,0.01):OnComplete(
			function()					
				PaintEventUI()
			end)
		
	else
		GOEventHint:SetActive(false)
		GOEventPatience.transform:Find("PatienceBG").gameObject:SetActive(false)
		GOEventPatience.transform:Find("Patience").gameObject:SetActive(false)
	end
end
function PaintEventUI()
	local patienceCnt = 0
	local PatienceGO = GOEventPatience.transform:Find("Patience")
	local cnt = PatienceGO:GetChildCount()
	for i = 1,cnt-1 do
		patienceCnt = patienceCnt + 1
		if patienceCnt <= cnt/3 then
			PatienceGO:GetChild(i):GetChild(0).gameObject:GetComponent(typeof(CS.ExImage)).color = GenColor(189,254,34,255)
		else
			if patienceCnt <= (cnt/3 * 2) then
				PatienceGO:GetChild(i):GetChild(0).gameObject:GetComponent(typeof(CS.ExImage)).color = GenColor(254,196,34,255)
			else
				PatienceGO:GetChild(i):GetChild(0).gameObject:GetComponent(typeof(CS.ExImage)).color = GenColor(254,34,74,255)
			end
		end
	end
end
function UpdateEventUI()
	local PatienceGO = GOEventPatience.transform:Find("Patience")
	PatienceGO.gameObject:GetComponent(typeof(CS.ExImage)).fillAmount = 1-(currentEvent.timer / currentEvent.info.eventTime) 
end
function OpenEventChoose()
	if currentEvent ~= nil and not isEventOpen and not isPausing then
		GOEventPage:SetActive(true)
		InitEventPage()
	end
end
function InitEventPage()
	isEventOpen = true
	--开启此界面时暂停游戏
	isPausing = true
	PlaySFX("openUI")
	GOEventPage.transform:Find("Main/Left/Tex_Title").gameObject:GetComponent(typeof(CS.ExText)).text = GetName(currentEvent.info.eventTitle) 
	GOEventPage.transform:Find("Main/Left/Tex_Content").gameObject:GetComponent(typeof(CS.ExText)):DOText(GetName(currentEvent.info.eventDes),0.5,true)
	if currentEvent.info.eventType == 1 then
		--外卖
		GOTakeoutIcon:SetActive(true)
		GOEventIcon:SetActive(false)
		GOTakeoutPart:SetActive(true)
		GOEventPart:SetActive(false)
		InitTakeoutPart()
	else
		--选择
		GOTakeoutIcon:SetActive(false)
		GOEventIcon:SetActive(true)
		GOTakeoutPart:SetActive(false)
		GOEventPart:SetActive(true)
		InitEventPart()
	end
end
function InitTakeoutPart()
	local cnt = 0
	takeoutPos = {0,0,0,0,0}
	takeoutBtn = {nil,nil,nil,nil,nil}
	for i=1,5 do
		if IsDishReady(i) then
			cnt = cnt + 1
			takeoutPos[cnt] = i
		end
	end
	GOTakeoutPart.transform:Find("Empty").gameObject:SetActive(cnt == 0)
	GOTakeoutPart.transform:Find("Layout").gameObject:SetActive(cnt ~= 0)
	if cnt <= 3 then
		GOTakeoutPart.transform:Find("Layout/SecondLine").gameObject:SetActive(false)		
	else
		GOTakeoutPart.transform:Find("Layout/SecondLine").gameObject:SetActive(true)		
	end
	TakeoutBtn1:SetActive(false)
	TakeoutBtn2:SetActive(false)
	TakeoutBtn3:SetActive(false)
	TakeoutBtn4:SetActive(false)
	TakeoutBtn5:SetActive(false)
	if cnt >= 1 then
		SetTakeoutBtn(TakeoutBtn1,1)
	end
	if cnt >= 2 then
		SetTakeoutBtn(TakeoutBtn2,2)
	end
	if cnt == 3 or cnt == 5 then
		SetTakeoutBtn(TakeoutBtn3,3)
	end
	if cnt == 4 then
		SetTakeoutBtn(TakeoutBtn4,3)
		SetTakeoutBtn(TakeoutBtn5,4)
	end
	if cnt == 5 then
		SetTakeoutBtn(TakeoutBtn4,4)
		SetTakeoutBtn(TakeoutBtn5,5)
	end
end
function SetTakeoutBtn(go,pos)
	go:SetActive(true)
	go.transform:Find("Img_Food"):GetComponent(typeof(CS.ExImage)).sprite = foodPicList[takeoutPos[pos]-1]
	go.transform:Find("Img_Corret").gameObject:SetActive(false)

	go.transform:Find("Tex_Score").gameObject:SetActive(false)
	go.transform:Find("Img_Mask").gameObject:SetActive(false)
	takeoutBtn[pos] = go
end
function OnClickTakeoutBtn(pos)
	if takeoutPos[pos] == currentEvent.info.eventDetail.requireDish then
		for i=1,#takeoutBtn do
			if takeoutBtn[i] ~= nil then
				if i == pos then
					takeoutBtn[i].transform:Find("Img_Corret").gameObject:SetActive(true)
					takeoutBtn[i].transform:Find("Tex_Score").gameObject:SetActive(true)
					takeoutBtn[i].transform:Find("Tex_Score").gameObject:GetComponent(typeof(CS.ExText)).text = currentEvent.info.eventDetail.bonus
				else
					takeoutBtn[i].transform:Find("Img_Mask").gameObject:SetActive(true)
				end
			end			
		end

		ResolveCurrentEvent(0)
		PlaySFX("eventSelRight")
	else
		CS.CommonController.LightMessageTips(GetName(60141))
		PlaySFX("eventSelWrong")
	end
end
function InitEventPart()
	
	local parentTrans = GOEventPart.transform:Find("Layout")
	if parentTrans:GetChildCount() > 1 then
		for i=1,parentTrans:GetChildCount() -1 do
			CS.UnityEngine.Object.Destroy(parentTrans:GetChild(i).gameObject)		
		end
	end
	--TableStruct2 = {des = "选项一,选项二",precheck = "0,0",effect = "1:100,1:500"}
	local optionsInfo = currentEvent.info.eventDetail
	local SplitArray = Split(optionsInfo.des,',')
	
	local precheckArray = Split(optionsInfo.precheck,',')
	for i=1,#SplitArray do
		local optionObj = CS.UnityEngine.Object.Instantiate(GOEventChooseItem,parentTrans,false)
		optionObj:SetActive(true)
		optionObj.transform:Find("Tex_Choose").gameObject:GetComponent(typeof(CS.ExText)).text = GetName(tonumber(SplitArray[i]))
		optionObj:GetComponent(typeof(CS.ExButton)).interactable = GetEventPrecheck(precheckArray[i])
		optionObj:GetComponent(typeof(CS.ExButton)).onClick:AddListener(
			function()
				PlaySFX("btn1")
				ResolveCurrentEvent(i)
			end)
	
	end
end
function ResolveCurrentEvent(sel)
	--未完成
	if currentEvent == nil then
		return
	end
	if sel == -1 then
		ResolveEventEffect(currentEvent.info.punish)
		currentEvent = nil
		RefreshEventUI()
		return 
	end
	--交付正确菜品
	if sel == 0 and currentEvent.info.eventType == 1 then
		RemoveDish(currentEvent.info.eventDetail.requireDish)
		SetScore(currentEvent.info.eventDetail.bonus)
		ResolveEventEffect(currentEvent.info.eventDetail.effect)
		takeoutEventFinishCnt = takeoutEventFinishCnt + 1
		if not EventWaitClose then
			EventWaitCloseTimer = 0
			EventWaitClose = true
		end
	end
	if currentEvent.info.eventType == 2 then
		local effectArray = Split(currentEvent.info.eventDetail.effect,';')
		local titleArray = Split(currentEvent.info.eventDetail.endEventTitle,',')
		local desArray = Split(currentEvent.info.eventDetail.endEventDes,',')
		ResolveEventEffect(effectArray[sel])
		FinishChangeEventPage(titleArray[sel],desArray[sel])
		if not EventWaitClose then
			EventWaitCloseTimer = 0
			EventWaitClose = true
		end

	end
	currentEvent = nil
	RefreshEventUI()
end
function ResolveEventEffect(str)
	if str == nil then return end
	--print('ResolveEventEffect '..str)
	--解析字符串
	local SplitArray = Split(str,',')
	for i=1,#SplitArray do
		if SplitArray[i] == '0' then
		
		else
			local strarray2 = Split(SplitArray[i],':')
			local effectType = tonumber(strarray2[1])
			local effectValue = tonumber(strarray2[2])
			EventEffect(effectType,effectValue)
		end
		
	end
end
function GetEventPrecheck(str)

	if str == '0' then
		return true
	else
		local strarray2 = Split(str,':')
		local effectType = tonumber(strarray2[1])
		local effectValue = tonumber(strarray2[2])
		--print('GetEventPrecheck '..tostring(EventSelectPrecheck(effectType,effectValue))..' '..effectType..' '..effectValue)
		return EventSelectPrecheck(effectType,effectValue)
	end
end
function FinishChangeEventPage(title,des)
	GOEventPage.transform:Find("Main/Left/Tex_Title").gameObject:GetComponent(typeof(CS.ExText)).text = GetName(tonumber(title))
	GOEventPage.transform:Find("Main/Left/Tex_Content").gameObject:GetComponent(typeof(CS.ExText)).text = ""
	GOEventPage.transform:Find("Main/Left/Tex_Content").gameObject:GetComponent(typeof(CS.ExText)):DOText(GetName(tonumber(des)),0.5,true)
end
function CloseEventPage()
	if isUIPausing then return end
	if not isEventOpen then return end

	--GOEventPage:SetActive(false)
	isEventOpen = false
	isPausing = false
	EventWaitClose = false
	RefreshEventUI()
	GOEventPage.transform:Find("Main").gameObject:GetComponents(typeof(CS.TweenPlay))[1].EndHandle = function()
		GOEventPage:SetActive(false)
	end
	GOEventPage.transform:Find("Main").gameObject:GetComponents(typeof(CS.TweenPlay))[1]:DoTween()
end
function EventSelectPrecheck(type,arg)
	local flag = false
	if type == 0 then
		flag = true
	end
	--检查原材料
	if type == 1 then
		if arg >0 and arg <= #IngredientInfo and IngredientInfo[arg].isReady then
			flag = true
		end
	end
	--检查菜肴
	if type == 2 then
		if arg >0 and arg <= 5 and  IsDishReady(arg) then
			flag = true
		end
	end
	--检查分数
	if type == 3 then
		if currentScore >= arg  then
			flag = true
		end
	end
	return flag
end	
function EventEffect(type,arg)
	if type == 1 then
		SetScore(-arg)
	end
	if type == 2 then
		SetScore(arg)
	end
	if type == 3 then
		AddTargetDishScoreMultiply(1,1,arg)
	end
	if type == 4 then
		AddTargetDishScoreMultiply(2,1,arg)
	end
	if type == 5 then
		AddTargetDishScoreMultiply(3,1,arg)
	end
	if type == 6 then
		AddTargetDishScoreMultiply(4,1,arg)
	end
	if type == 7 then
		AddTargetDishScoreMultiply(5,1,arg)
	end
	if type == 8 then
		AddIngredientbuff(arg,10)
	end
	if type == 9 then
		RecoverCustomerPatience(arg)
	end
	if type == 10 then
		GainExtraIngredient(arg)
	end
	if type == 11 then
		Player1Disable = true
		player1DisableTimer = arg
		UpdateIngredientCookingUI()
		UpdatePlayerSpineAnim()
	end
	if type == 12 then
		Player2Disable = true
		player2DisableTimer = arg
		UpdateIngredientCookingUI()
		UpdatePlayerSpineAnim()
	end
	if type == 13 then
		GenNewCustomer(-1)
	end
	if type == 14 then
		AddAnyScoreMultiply(2,arg)
	end
	if type == 15 then
		RemoveEventFromEventPool(arg)
	end
	if type == 16 then
		AddEventToEventPool(arg)
	end
	if type == 17 then
		AddIngredientbuff(arg,5)
	end
	if type == 18 then
		AddTargetDishScoreFixed(1,arg,1)
	end
	if type == 19 then
		AddTargetDishScoreFixed(2,arg,1)
	end
	if type == 20 then
		AddTargetDishScoreFixed(3,arg,1)
	end
	if type == 21 then
		AddTargetDishScoreFixed(4,arg,1)
	end
	if type == 22 then
		AddTargetDishScoreFixed(5,arg,1)
	end
	if type == 23 then
		local rnd = math.random(0,100)
		if rnd >= 50 then
			SetScore(arg)
			CS.CommonController.LightMessageTips(GetName(60263))
		else
			SetScore(-50)
			CS.CommonController.LightMessageTips(GetName(60264))
		end
	end
	
end
----------------结算界面---------------------
function ClearGame()
	FinishGame()
end
function StartOpenResultPage()
	waitOpenResultPage = true
	
end
local isResultOpen = false
function OpenResultPage()
	if isResultOpen then return end
	isResultOpen = true
	ClearAllOrder()
	PlaySFX("stopcook")
	PlaySFX("resultMedal")
	ResultGO:SetActive(true)
	isOpenResultPageCD = true
	if stageNum <= 5 then
		ResultGO.transform:Find("Frame/Day"):GetChild(stageNum-1).gameObject:SetActive(true)
	else
		ResultGO.transform:Find("Frame/Day"):GetChild(4).gameObject:SetActive(true)
	end
	if CS.GameData.userInfo ~= nil then
		ResultGO.transform:Find("Frame/Tex_Name").gameObject:GetComponent(typeof(CS.ExText)).text = CS.GameData.userInfo.name
		ResultGO.transform:Find("Frame/Tex_UID").gameObject:GetComponent(typeof(CS.ExText)).text = CS.GameData.userInfo.userId
	end
	local lastTime = globalTimer
	local countdownMinute = math.modf(lastTime / 60)
	local countdownSec = math.modf(lastTime - countdownMinute * 60) 
	ResultGO.transform:Find("Frame/Tex_Time").gameObject:GetComponent(typeof(CS.ExText)).text  = string.format("%02d",(countdownMinute))..":"..string.format("%02d",(countdownSec))
	SetOrderResult(ResultOrderLv3,lvl3CustomerCnt)
	SetOrderResult(ResultOrderLv2,lvl2CustomerCnt)
	SetOrderResult(ResultOrderLv1,lvl1CustomerCnt)
	SetOrderResult(ResultOrderEX,takeoutEventFinishCnt)
	if stageNum <= 4 then
		isOpenResultPage = true
		ResultGO.transform:Find("Frame/Tex_Score").gameObject:GetComponent(typeof(CS.ExText)).text = currentScore ..'/'.. TargetScore
		ResultGO.transform:Find("Frame/Tex_Score").gameObject:SetActive(true)
	else
		ResultGO.transform:Find("Frame/Tex_Score").gameObject:GetComponent(typeof(CS.ExText)).text = currentScore
		local rank = GetEndlessRank()	
		--ResultGO.transform:Find("Frame/Img_Level").gameObject:SetActive(true)	
		ResultGO.transform:Find("Frame/Img_Level").gameObject:GetComponent(typeof(CS.ExImage)).sprite = resultEndlessPicList[rank-1]
		OrderResultScoreAnim(rank)
		PlaySFX("resultSuccess")
	end
end
function SetOrderResult(go,cnt)
	go:SetActive(true)
	go.transform:Find("Tex_Num").gameObject:GetComponent(typeof(CS.ExText)).text = tostring(cnt)
end
function OrderResultScoreAnim(rank,percent)
	local seq = CS.DG.Tweening.DOTween.Sequence()
	if rank >= 1 then
		local amount = 1
		if rank == 1 then amount = currentScore/5400 end
		seq:Append(ResultGO.transform:Find("Frame/LevelBar/Img_D").gameObject:GetComponent(typeof(CS.ExImage)):DOFillAmount(amount,0.5):SetDelay(1.6))
	end
	if rank >= 2 then
		local amount = 1
		if rank == 2 then amount = (currentScore-5400)/(10100-5400) end
		seq:Append(ResultGO.transform:Find("Frame/LevelBar/Img_C").gameObject:GetComponent(typeof(CS.ExImage)):DOFillAmount(amount,0.5))
	end
	if rank >= 3 then
		local amount = 1
		if rank == 3 then amount = (currentScore-10100)/(13500-10100) end
		seq:Append(ResultGO.transform:Find("Frame/LevelBar/Img_B").gameObject:GetComponent(typeof(CS.ExImage)):DOFillAmount(amount,0.5))
	end
	if rank >= 4 then
		local amount = 1
		if rank == 4 then amount = (currentScore-13500)/(17300-13500) end
		seq:Append(ResultGO.transform:Find("Frame/LevelBar/Img_A").gameObject:GetComponent(typeof(CS.ExImage)):DOFillAmount(amount,0.5))
	end
	if rank >= 5 then
		seq:Append(ResultGO.transform:Find("Frame/LevelBar/Img_S").gameObject:GetComponent(typeof(CS.ExImage)):DOFillAmount(1,0.5))
	end
	seq:OnComplete(
		function()					
			ResultGO.transform:Find("Frame/Tex_Score").gameObject:SetActive(true)
			ResultGO.transform:Find("Frame/Img_Level").gameObject:SetActive(true)
			isOpenResultPage = true
			openResultPageTimer = 1.61
		end):Play()
end
function GetEndlessRank()
	if currentScore >= 17300 then
		return 5
	end
	if currentScore >= 13500 then
		return 4
	end
	if currentScore >= 10100 then
		return 3
	end
	if currentScore >= 5400 then
		return 2
	end
	if currentScore >= 0 then
		return 1
	end
end
----------------便捷函数---------------------
function IsDishReady(id)
	return foodPos1 == id or foodPos2 == id or foodPos3 == id or (Cooker1Holding == id and isCooker1Cooking == false) or (Cooker2Holding == id and isCooker2Cooking == false)
end
function RemoveDish(dishid)
		local flag = false
		if foodPos1 == dishid then
			foodPos1 = 0
			RefreshFoodPos()
			flag = true
			return flag	
		end
		if foodPos2 == dishid then
			foodPos2 = 0
			RefreshFoodPos()
			flag = true
			return flag	
		end
		if foodPos3 == dishid then
			foodPos3 = 0
			RefreshFoodPos()
			flag = true
			return flag	
		end
		if Cooker1Holding == dishid and not isCooker1Cooking then
			Cooker1Holding = 0
			RefreshFoodPos()
			flag = true
			return flag	
		end
		if Cooker2Holding == dishid and not isCooker2Cooking then
			Cooker2Holding = 0
			RefreshFoodPos()
			flag = true
			return flag	
		end
		return flag	
end
function HaveDish(dishid)
		local flag = false
		if foodPos1 == dishid then
			flag = true
			return flag	
		end
		if foodPos2 == dishid then
			flag = true
			return flag	
		end
		if foodPos3 == dishid then
			flag = true
			return flag	
		end
		if Cooker1Holding == dishid and not isCooker1Cooking then
			flag = true
			return flag	
		end
		if Cooker2Holding == dishid and not isCooker2Cooking then
			flag = true
			return flag	
		end
		return flag	
	end
function DestroyChildren(transform)
	for i=0,transform.childCount-1 do
		CS.UnityEngine.Object.Destroy(transform:GetChild(i).gameObject)
	end
	return 
end

function Split(szFullString, szSeparator)
	if(szFullString == nil) then
		return nil
	end
	local nFindStartIndex = 0
	local nSplitIndex = 1
	local nSplitArray = {}
	while true do
		local nFindLastIndex = string.find(szFullString, szSeparator, nFindStartIndex)
		if not nFindLastIndex then
			nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, string.len(szFullString))
			break
		end
		nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, nFindLastIndex - 1)
		nFindStartIndex = nFindLastIndex + string.len(szSeparator)
		nSplitIndex = nSplitIndex + 1
	end
	return nSplitArray
end


function GenColor(r,g,b,a)
	if(r<=1 and g<=1 and b<=1 and a<=1) then	
		return CS.UnityEngine.Color(r,g,b,a)
	else
		return CS.UnityEngine.Color(r/255,g/255,b/255,a/255)
	end
end



function PlaySFX(FXname)
	--print(FXname)
	if FXname == "cook" then
		CS.CommonAudioController.PlayUI("UI_Cooking")
	end
	if FXname == "cookFinish" then
		CS.CommonAudioController.PlayUI("UI_Cooking_Done")
	end
	if FXname == "newCustomer" then
		CS.CommonAudioController.PlayUI("UI_Doorbell")
	end
	if FXname == "ingredientCut" then
		CS.CommonAudioController.PlayUI("UI_Food_Cut")
	end
	if FXname == "ingredientBoil" then
		CS.CommonAudioController.PlayUI("UI_Frying_Boiling")
	end
	if FXname == "ingredientSel" then
		CS.CommonAudioController.PlayUI("UI_Food_Impact")
	end
	if FXname == "openUI" then
		CS.CommonAudioController.PlayUI("UI_Menu_Open")
	end
	if FXname == "newEvent" then
		CS.CommonAudioController.PlayUI("UI_Takeout_Tip")
	end
	if FXname == "customerLeave" then
		CS.CommonAudioController.PlayUI("UI_Appraise_Dissatisfied")
	end
	if FXname == "customerFinish" then
		CS.CommonAudioController.PlayUI("UI_Appraise_Satisfied")
	end
	if FXname == "eventSelWrong" then
		CS.CommonAudioController.PlayUI("UI_Select_Wrong")
	end
	if FXname == "eventSelRight" then
		CS.CommonAudioController.PlayUI("UI_Select_Right")
	end
	if FXname == "stopcook" then
		CS.CommonAudioController.PlayUI("Stop_UI_loop")
	end
	if FXname == "btn1" then
		CS.CommonAudioController.PlayUI("UI_selete_2")
	end
	if FXname == "btnCancel" then
		CS.CommonAudioController.PlayUI("UI_cancel")
	end
	if FXname == "resultSuccess" then
		CS.CommonAudioController.PlayUI("UI_Audit_Success")
	end
	if FXname == "resultFail" then
		CS.CommonAudioController.PlayUI("UI_Audit_Defeat")
	end
	if FXname == "resultStamp" then
		CS.CommonAudioController.PlayUI("UI_Audit_Stamp")
	end
	if FXname == "CountDown" then
		CS.CommonAudioController.PlayBattle("FlightGame_Audio_LastTime")
	end
	if FXname == "resultMedal" then
		CS.CommonAudioController.PlayUI("UI_medal")
	end
	
end

function GetName(NameID)
	return CS.Data.GetLang((NameID))
end
function GenColor(r,g,b,a)
	if(r<=1 and g<=1 and b<=1 and a<=1) then	
		return CS.UnityEngine.Color(r,g,b,a)
	else
		return CS.UnityEngine.Color(r/255,g/255,b/255,a/255)
	end
end
function FinishGame()
	local BattleController = CS.GF.Battle.BattleController.Instance
	
	for i=BattleController.enemyTeamHolder.listCharacter.Count-1,0,-1 do
		local DamageInfo = CS.GF.Battle.BattleDamageInfo()
		if BattleController.enemyTeamHolder.listCharacter[i] ~= nil then
			BattleController.enemyTeamHolder.listCharacter[i]:UpdateLife(DamageInfo, -999999)
		end
	end
	CS.BattleFrameManager.ResumeTime()
	CS.UnityEngine.Object.Destroy(ResultGO)
	CS.UnityEngine.Object.Destroy(self.gameObject)
end
function ExitGame()
	CS.BattleFrameManager.ResumeTime()
	CS.GF.Battle.BattleController.Instance:TriggerBattleFinishEvent(true)
	--for i=0,BattleController.enemyTeamHolder.listCharacter.Count-1 do
	--	local DamageInfo = CS.GF.Battle.BattleDamageInfo()
	--	BattleController.enemyTeamHolder.listCharacter[i]:UpdateLife(DamageInfo, -999999)
	--end
	CS.UnityEngine.Object.Destroy(self.gameObject)
end
function GetEmojiSprite(code)
	return CS.CommonController.LoadPngCreateSprite("Pics/Icons/Emoji/" .. code);
end
function GetEndlessTime(wave)
	if wave <= 18 then
		return endlessTimeInfo[wave]
	else
		return endlessTimeInfo[18] + (wave-18) * 30
	end
end
function GetEndlessScore(wave)
	if wave <= 18 then
		return endlessScoreInfo[wave]
	else
		return math.floor((GetEndlessTime(wave) * 10 * 3 / 100)) * 100
	end
end
function CheckEndlessWave()
	if currentScore >= GetEndlessScore(curEndlessWave) then
		curEndlessWave = curEndlessWave + 1
		SetTargetScore(GetEndlessScore(curEndlessWave),false)
		SetTimeLimit(GetEndlessTime(curEndlessWave),GetEndlessTime(curEndlessWave) - GetEndlessTime(curEndlessWave-1))
	else
		waitOpenResultPage = true
	end
end
function SetTimeLimit(time,diff)
	timeLimit = time
	local countdownMinute = math.modf(diff / 60)
	local countdownSec = math.modf(diff - countdownMinute * 60)
	TextTime.transform:GetChild(0).gameObject:GetComponent(typeof(CS.ExText)).text = '+'.. string.format("%02d",(countdownMinute))..":"..string.format("%02d",(countdownSec))
	TextTime.transform:GetChild(0).gameObject:SetActive(false)
	TextTime.transform:GetChild(0).gameObject:SetActive(true) 
end
function GetOrderGO(pos)
	if stageNum ~= 4 then
		if pos == 1 then
			return GoOrder1
		end
		if pos == 2 then
			return GoOrder2
		end
		if pos == 3 then
			return GoOrder3
		end
		if pos == 4 then
			return GoOrder4
		end
	else
		if pos == 1 then
			return GoOrder1Boss
		end
		if pos == 2 then
			return GoOrder2Boss
		end
		if pos == 3 then
			return GoOrder3Boss
		end
		if pos == 4 then
			return GoOrder4Boss
		end
	end
end

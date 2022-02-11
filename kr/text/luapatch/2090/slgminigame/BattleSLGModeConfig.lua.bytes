minigameEnemyGroupID = {513701,513702,513703,513704}
--
friendlyAreaOffset = CS.UnityEngine.Vector3(0,0,-0.7) -- 友方区域偏移
CameraStaticOffset = CS.UnityEngine.Vector3(-1,12,-22.5) --摄像机位置
camaraStaticRotation = 30
--
gridHorizontalAmount = {33,43,48,48} --横向数量
gridVerticalAmount = 9
gridwidth = 1.5 --格子宽度
gridheight = 1.7 -- 格子高度
--
startingResourcePoint = {8,1,0,0} --行动点初始值
resourcePointMax = {8,8,8,10}--行动点最大值
RPRengenTimeFrame = 240
resourcePointMoveCost = 0
--
stageStrategyGunID = {9095,9089,9096,9097}
stageStrategySkills = {{118302,118309},{118302,118309},{118302,118309,118301},{118302,118309,118301}}
--
friendlyStartingPos = {}
--
tableStruct = {}

--
SLGSkills = {}
--
SLGEnemyMoves = {}
--
SLGEnemyGroupData = {}
SLGEnemyGroupMoveGroup = {}
local configFunction = {}
function configFunction:InitData(stageid)
	--print(stageid)
	if stageid == 1 then
		friendlyStartingPos[1] = CS.UnityEngine.Vector2Int(3,3)
		
	end
	if stageid == 2 then
		friendlyStartingPos[1] = CS.UnityEngine.Vector2Int(4,2)
		friendlyStartingPos[2] = CS.UnityEngine.Vector2Int(5,4)
		friendlyStartingPos[3] = CS.UnityEngine.Vector2Int(3,7)
	end
	if stageid == 3 then
		friendlyStartingPos[1] = CS.UnityEngine.Vector2Int(19,3)
		friendlyStartingPos[2] = CS.UnityEngine.Vector2Int(20,3)
		friendlyStartingPos[3] = CS.UnityEngine.Vector2Int(19,2)
		friendlyStartingPos[4] = CS.UnityEngine.Vector2Int(19,5)
		friendlyStartingPos[5] = CS.UnityEngine.Vector2Int(19,4)
	end
	if stageid == 4 then
		friendlyStartingPos[1] = CS.UnityEngine.Vector2Int(19,3)
		friendlyStartingPos[2] = CS.UnityEngine.Vector2Int(20,3)
		friendlyStartingPos[3] = CS.UnityEngine.Vector2Int(19,2)
		friendlyStartingPos[4] = CS.UnityEngine.Vector2Int(19,5)
		friendlyStartingPos[5] = CS.UnityEngine.Vector2Int(19,4)
	end
	tableStruct = {id = 1 ,skillid = 11810601,skilltype = 3,skillrange = 5,skillcost = 3,spcost = 1}
	SLGSkills[tableStruct.id] = tableStruct
	
	tableStruct = {id = 2 ,skillid = 11810501,skilltype = 1,skillrange = 4,skillcost = 1,spcost = 0}
	SLGSkills[tableStruct.id] = tableStruct
	
	tableStruct = {id = 3 ,skillid = 10211210,skilltype = 3,skillrange = 3,skillcost = 1,spcost = 0}
	SLGSkills[tableStruct.id] = tableStruct
	
	tableStruct = {id = 4 ,skillid = 11815501,skilltype = 1,skillrange = 3,skillcost = 1,spcost = 0}
	SLGSkills[tableStruct.id] = tableStruct
	
	tableStruct = {id = 5 ,skillid = 11830101,skilltype = 0,skillrange = 999,skillcost = 1,spcost = 0}--加移速
	SLGSkills[tableStruct.id] = tableStruct

	tableStruct = {id = 6 ,skillid = 11830201,skilltype = 0,skillrange = 999,skillcost = 2,spcost = 0}--加射程
	SLGSkills[tableStruct.id] = tableStruct
	
	tableStruct = {id = 7 ,skillid = 11815401,skilltype = 0,skillrange = 999,skillcost = -10,spcost = 0}
	SLGSkills[tableStruct.id] = tableStruct
	
	tableStruct = {id = 8 ,skillid = 11813401,skilltype = 3,skillrange = 6,skillcost = 1,spcost = 0}
	SLGSkills[tableStruct.id] = tableStruct
	
	tableStruct = {id = 9 ,skillid = 11813301,skilltype = 1,skillrange = 3,skillcost = 1,spcost = 0}
	SLGSkills[tableStruct.id] = tableStruct
	
	tableStruct = {id = 10 ,skillid = 11812801,skilltype = 1,skillrange = 8,skillcost = 1,spcost = 0}
	SLGSkills[tableStruct.id] = tableStruct
	
	tableStruct = {id = 11 ,skillid = 11812901,skilltype = 1,skillrange = 8,skillcost = 2,spcost = 0}
	SLGSkills[tableStruct.id] = tableStruct

	tableStruct = {id = 12 ,skillid = 11830701,skilltype = 0,skillrange = 999,skillcost = 1,spcost = 0}--炸幻象眩晕
	SLGSkills[tableStruct.id] = tableStruct

	tableStruct = {id = 13 ,skillid = 11830801,skilltype = 0,skillrange = 999,skillcost = 2,spcost = 0}--嗜血术
	SLGSkills[tableStruct.id] = tableStruct

	tableStruct = {id = 14 ,skillid = 11830901,skilltype = 0,skillrange = 999,skillcost = 4,spcost = 0}--意大利炮
	SLGSkills[tableStruct.id] = tableStruct

	tableStruct = {id = 15 ,skillid = 11816801,skilltype = 0,skillrange = 6,skillcost = 1,spcost = 0}
	SLGSkills[tableStruct.id] = tableStruct

	tableStruct = {id = 16 ,skillid = 11816901,skilltype = 0,skillrange = 6,skillcost = 2,spcost = 0}
	SLGSkills[tableStruct.id] = tableStruct
	------------------------------------------------------
	------------------------------------------------------		
	local tableStructPoint = {}
	local tableStructNum = {}
	
	tableStruct = {id = 0, isMove = false,isLoop = false, movePoints = nil,waitFrames = nil}
	SLGEnemyMoves[tableStruct.id] = tableStruct 	

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(7,7)
	tableStructNum[1] = 60
	tableStruct = {id = 1, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(6,6)
	tableStructNum[1] = 240
	tableStruct = {id = 2, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(18,1)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(18,3)
	tableStructNum[1] = 60
	tableStructNum[2] = 57
	tableStruct = {id = 3, isMove = true, isLoop = true, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(18,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(18,5)
	tableStructNum[1] = 60
	tableStructNum[2] = 60
	tableStruct = {id = 4, isMove = true, isLoop = true, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(19,1)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(19,3)
	tableStructNum[1] = 60
	tableStructNum[2] = 57
	tableStruct = {id = 5, isMove = true, isLoop = true, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(19,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(19,5)
	tableStructNum[1] = 60
	tableStructNum[2] = 60
	tableStruct = {id = 6, isMove = true, isLoop = true, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(20,1)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(20,3)
	tableStructNum[1] = 60
	tableStructNum[2] = 57
	tableStruct = {id = 7, isMove = true, isLoop = true, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(20,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(20,5)
	tableStructNum[1] = 60
	tableStructNum[2] = 60
	tableStruct = {id = 8, isMove = true, isLoop = true, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
			
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(8,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(5,5)
	tableStructNum[1] = 120
	tableStructNum[2] = 120
	tableStruct = {id = 9, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
				
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(7,3)
	tableStructNum[1] = 60
	tableStruct = {id = 10, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,7)--                                                           不同波次移动至（1,7）
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)
	tableStructNum[1] = 60
	tableStruct = {id = 11, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)
	tableStructNum[1] = 450
	tableStruct = {id = 12, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)
	tableStructNum[1] = 960
	tableStruct = {id = 13, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)
	tableStructNum[1] = 1410
	tableStruct = {id = 14, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)
	tableStructNum[1] = 1860
	tableStruct = {id = 15, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)
	tableStruct = {id = 16, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,6)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)--                                                           不同波次移动至（1,6）
	tableStructNum[1] = 60
	tableStruct = {id = 17, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,6)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)
	tableStructNum[1] = 450
	tableStruct = {id = 18, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,6)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)
	tableStructNum[1] = 960
	tableStruct = {id = 19, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,6)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)
	tableStructNum[1] = 1410
	tableStruct = {id = 20, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,6)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)
	tableStructNum[1] = 1860
	tableStruct = {id = 21, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,6)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)
	tableStructNum[1] = 2310
	tableStruct = {id = 22, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)--                                                           不同波次移动至(1,5)
	tableStructNum[1] = 60
	tableStruct = {id = 23, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)
	tableStructNum[1] = 450
	tableStruct = {id = 24, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)
	tableStructNum[1] = 960
	tableStruct = {id = 25, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)
	tableStructNum[1] = 1410
	tableStruct = {id = 26, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)
	tableStructNum[1] = 1860
	tableStruct = {id = 27, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)
	tableStructNum[1] = 2310
	tableStruct = {id = 28, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,4)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)--                                                           不同波次移动至(1,4)
	tableStructNum[1] = 60
	tableStruct = {id = 29, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,4)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)
	tableStructNum[1] = 450
	tableStruct = {id = 30, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,4)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)
	tableStructNum[1] = 960
	tableStruct = {id = 31, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,4)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)
	tableStructNum[1] = 1410
	tableStruct = {id = 32, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,4)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)
	tableStructNum[1] = 1860
	tableStruct = {id = 33, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,4)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)
	tableStructNum[1] = 2310
	tableStruct = {id = 34, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}--P1杂鱼1
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,2)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,2)
	tableStructNum[1] = 60
	tableStruct = {id = 35, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
			
	tableStructPoint = {}--P1杂鱼2
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,3)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,3)
	tableStructNum[1] = 60
	tableStruct = {id = 36, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
			
	tableStructPoint = {}--P1杂鱼3
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,4)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)
	tableStructNum[1] = 60
	tableStruct = {id = 37, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
			
	tableStructPoint = {}--P1杂鱼4
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)
	tableStructNum[1] = 210
	tableStruct = {id = 38, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
			
	tableStructPoint = {}--P1杂鱼5
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,6)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)
	tableStructNum[1] = 210
	tableStruct = {id = 39, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
				
	tableStructPoint = {}--P1杂鱼6
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)
	tableStructNum[1] = 210
	tableStruct = {id = 40, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}--P1杂鱼7
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,2)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,2)
	tableStructNum[1] = 510
	tableStruct = {id = 41, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
			
	tableStructPoint = {}--P1杂鱼8
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,3)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,3)
	tableStructNum[1] = 510
	tableStruct = {id = 42, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
			
	tableStructPoint = {}--P1杂鱼9
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,4)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)
	tableStructNum[1] = 510
	tableStruct = {id = 43, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
			
	tableStructPoint = {}--P1杂鱼10
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)
	tableStructNum[1] = 660
	tableStruct = {id = 44, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
			
	tableStructPoint = {}--P1杂鱼11
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,6)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)
	tableStructNum[1] = 660
	tableStruct = {id = 45, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
				
	tableStructPoint = {}--P1杂鱼12
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)
	tableStructNum[1] = 660
	tableStruct = {id = 46, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--P1杂鱼1-斜侧底线
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,2)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,9)
	tableStructNum[1] = 960
	tableStruct = {id = 47, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}--P2杂鱼2-斜侧底线
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,3)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,8)
	tableStructNum[1] = 960
	tableStruct = {id = 48, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
			
	tableStructPoint = {}--P2杂鱼3-斜侧底线
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,6)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,2)
	tableStructNum[1] = 960
	tableStruct = {id = 49, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}--P2杂鱼4-斜侧底线
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(33,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,3)
	tableStructNum[1] = 960
	tableStruct = {id = 50, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--黑狙1号-22s
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(1,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)
	tableStructNum[1] = 1110
	tableStruct = {id = 51, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--黑狙2号-25s
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,1)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,1)
	tableStructNum[1] = 1110
	tableStruct = {id = 52, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--黑狙3号-25s
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,8)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,8)
	tableStructNum[1] = 1110
	tableStruct = {id = 53, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}--黑狙4号-22s
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(27,4)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,8)
	tableStructNum[1] = 1110
	tableStruct = {id = 54, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}--黑狙5号-35s
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(28,3)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,3)
	tableStructNum[1] = 1470
	tableStruct = {id = 55, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}--黑狙6号-35s
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(28,4)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)
	tableStructNum[1] = 1470
	tableStruct = {id = 56, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}--黑狙7号-35s
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(28,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)
	tableStructNum[1] = 1470
	tableStruct = {id = 57, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}--黑狙8号-35s
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(28,6)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)
	tableStructNum[1] = 1470
	tableStruct = {id = 58, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--P3-白指挥1
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(26,3)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)
	tableStructNum[1] = 2010
	tableStruct = {id = 59, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--P3-白指挥2
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(26,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)
	tableStructNum[1] = 2010
	tableStruct = {id = 60, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--P3-黑狙9
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(27,4)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(24,4)
	tableStructPoint[3] = CS.UnityEngine.Vector2Int(1,4)	
	tableStructNum[1] = 2010
	tableStruct = {id = 61, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--P3-黑狙10
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(27,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(24,5)
	tableStructPoint[3] = CS.UnityEngine.Vector2Int(1,5)	
	tableStructNum[1] = 2010
	tableStruct = {id = 62, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--P3-杂鱼17
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,2)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,2)	
	tableStructNum[1] = 1920
	tableStruct = {id = 63, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 		

	tableStructPoint = {}--P3-杂鱼18
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,8)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)	
	tableStructNum[1] = 1920
	tableStruct = {id = 64, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P3-杂鱼19
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,2)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,3)		
	tableStructNum[1] = 1920
	tableStruct = {id = 65, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}--P3-杂鱼20
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,3)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)		
	tableStructNum[1] = 1920
	tableStruct = {id = 66, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}--P3-杂鱼21
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,6)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)	
	tableStructNum[1] = 1920
	tableStruct = {id = 67, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--P3-杂鱼22
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,7)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)
	tableStructNum[1] = 1920
	tableStruct = {id = 68, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--P4-掷弹士
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(27,3)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)		
	tableStructNum[1] = 2910
	tableStruct = {id = 69, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--P4-杂鱼23
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,2)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,2)		
	tableStructNum[1] = 2910
	tableStruct = {id = 70, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--P4-杂鱼24
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,3)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,3)		
	tableStructNum[1] = 2910
	tableStruct = {id = 71, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 		

	tableStructPoint = {}--P4-杂鱼25
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,4)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)		
	tableStructNum[1] = 2910
	tableStruct = {id = 72, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P4-杂鱼26
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)		
	tableStructNum[1] = 3060
	tableStruct = {id = 73, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P4-杂鱼27
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,6)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)
	tableStructNum[1] = 3060
	tableStruct = {id = 74, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P4-杂鱼28
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)		
	tableStructNum[1] = 3060
	tableStruct = {id = 75, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--P4-杂鱼29
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,2)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,2)		
	tableStructNum[1] = 3210
	tableStruct = {id = 76, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--P4-杂鱼30
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,3)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,3)	
	tableStructNum[1] = 3210
	tableStruct = {id = 77, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 		

	tableStructPoint = {}--P4-杂鱼31
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,4)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)
	tableStructNum[1] = 3210
	tableStruct = {id = 78, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P4-杂鱼32
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)	
	tableStructNum[1] = 3360
	tableStruct = {id = 79, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P4-杂鱼33
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,6)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)	
	tableStructNum[1] = 3360
	tableStruct = {id = 80, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P4-杂鱼34
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)	
	tableStructNum[1] = 3360
	tableStruct = {id = 81, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P5-杂鱼35
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,2)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,2)
	tableStructNum[1] = 4260
	tableStruct = {id = 82, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P5-杂鱼36
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(1,3)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,3)
	tableStructNum[1] = 4260
	tableStruct = {id = 83, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P5-杂鱼37
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,4)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)	
	tableStructNum[1] = 4260
	tableStruct = {id = 84, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P5-杂鱼38
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,6)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)	
	tableStructNum[1] = 4500
	tableStruct = {id = 85, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P5-杂鱼39
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,7)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)	
	tableStructNum[1] = 4500
	tableStruct = {id = 86, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P5-杂鱼40
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,8)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,8)		
	tableStructNum[1] = 4500
	tableStruct = {id = 87, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P6-白指挥3
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(27,2)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)		
	tableStructNum[1] = 4800
	tableStruct = {id = 88, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}--P6-白指挥4
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(25,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,2)		
	tableStructNum[1] = 4800
	tableStruct = {id = 89, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}--P6-黑狙13
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,1)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,2)		
	tableStructNum[1] = 4800
	tableStruct = {id = 90, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
			
	tableStructPoint = {}--P6-黑狙14
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,8)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)		
	tableStructNum[1] = 4800
	tableStruct = {id = 91, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P6-杂鱼41
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,2)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,2)		
	tableStructNum[1] = 4800
	tableStruct = {id = 92, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--P6-杂鱼42
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,3)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,3)	
	tableStructNum[1] = 4800
	tableStruct = {id = 93, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 		

	tableStructPoint = {}--P6-杂鱼43
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,4)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)
	tableStructNum[1] = 4800
	tableStruct = {id = 94, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P6-杂鱼44
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)	
	tableStructNum[1] = 4800
	tableStruct = {id = 95, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P6-杂鱼45
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,6)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)	
	tableStructNum[1] = 4800
	tableStruct = {id = 96, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P6-杂鱼46
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)	
	tableStructNum[1] = 4800
	tableStruct = {id = 97, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--P7-掷弹手2
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(43,4)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)	
	tableStructNum[1] = 5550
	tableStruct = {id = 98, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P7-掷弹手3
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(43,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)	
	tableStructNum[1] = 5550
	tableStruct = {id = 99, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}--P7-白指挥5
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(26,3)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,3)	
	tableStructNum[1] = 5850
	tableStruct = {id = 100, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
			
	tableStructPoint = {}--P7-白指挥6
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(27,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)	
	tableStructNum[1] = 5550
	tableStruct = {id = 101, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
				
	tableStructPoint = {}--P7-黑狙15
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,2)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,2)	
	tableStructNum[1] = 5550
	tableStruct = {id = 102, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
				
	tableStructPoint = {}--P7-黑狙16
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)	
	tableStructNum[1] = 5550
	tableStruct = {id = 103, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
		
	tableStructPoint = {}--P6-杂鱼47
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,2)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,2)		
	tableStructNum[1] = 5700
	tableStruct = {id = 104, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 

	tableStructPoint = {}--P7-杂鱼48
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,3)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,3)	
	tableStructNum[1] = 5700
	tableStruct = {id = 105, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 		

	tableStructPoint = {}--P7-杂鱼49
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,4)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,4)
	tableStructNum[1] = 5700
	tableStruct = {id = 106, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P7-杂鱼50
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,5)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,5)	
	tableStructNum[1] = 5850
	tableStruct = {id = 107, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P7-杂鱼51
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,6)	
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,6)	
	tableStructNum[1] = 5850
	tableStruct = {id = 108, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	
	tableStructPoint = {}--P7-杂鱼52
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,7)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,7)	
	tableStructNum[1] = 5850
	tableStruct = {id = 109, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 	
		
	tableStructPoint = {}--P4-黑狙11
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,1)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,1)	
	tableStructNum[1] = 3210
	tableStruct = {id = 110, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
			
	tableStructPoint = {}--P4-黑狙12
	tableStructNum = {}
	tableStructPoint[1] = CS.UnityEngine.Vector2Int(35,8)
	tableStructPoint[2] = CS.UnityEngine.Vector2Int(1,8)	
	tableStructNum[1] = 3210
	tableStruct = {id = 111, isMove = true, isLoop = false, movePoints = tableStructPoint,waitFrames = tableStructNum}
	SLGEnemyMoves[tableStruct.id] = tableStruct 
	------------------------------------------------------
	------------------------------------------------------
	local SLGEnemyGroupMoveGroup1 = {9,10,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0}
	local SLGEnemyGroupMoveGroup2 = {0,0,0,0,1,2,3,4,0,5,6,7,0,8,0,0,0,0,0,0,0,0,0,0,0,0,0,0}
	local SLGEnemyGroupMoveGroup3 = {35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,71,72,73,74,77,78,79,80,75}
	local SLGEnemyGroupMoveGroup4 = {36,37,38,39,42,43,44,45,47,48,49,50,51,52,53,54,55,56,57,58,59,60,61,62,63,64,65,66,67,68,69,73,74,75,76,77,78,110,111,82,83,84,85,86,87,88,89,90,91,92,93,94,95,96,97,98,99,100,101,102,103,104,105,106,107,108,109,72}
	tableStruct = {id = 1, enemyGroupid = 513701, moveGroup = SLGEnemyGroupMoveGroup1}
	SLGEnemyGroupData[tableStruct.id] = tableStruct 
	tableStruct = {id = 2, enemyGroupid = 513702, moveGroup = SLGEnemyGroupMoveGroup2}
	SLGEnemyGroupData[tableStruct.id] = tableStruct 
	tableStruct = {id = 3, enemyGroupid = 513703, moveGroup = SLGEnemyGroupMoveGroup3}
	SLGEnemyGroupData[tableStruct.id] = tableStruct 
	tableStruct = {id = 4, enemyGroupid = 513704, moveGroup = SLGEnemyGroupMoveGroup4}
	SLGEnemyGroupData[tableStruct.id] = tableStruct 
end
return configFunction

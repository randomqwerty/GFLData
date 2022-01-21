local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentController)
xlua.private_accessible(CS.GameData)

playSpotTeamCapture = 0;
local InitTeamSpots = function(self)
	self:InitTeamSpots();
	if not CS.DeploymentBackgroundController.currentLayerData == nil then
		CS.DeploymentBackgroundController.Instance:ShowShade(true);
	end
	--CS.DeploymentController.InitBGM();
end

local CheckResult = function()
	CS.DeploymentController.Instance:CheckBattle();
end
local BuildCastSkillOnDeathHandler = function(self,data)
	self:BuildCastSkillOnDeathHandler(data);
	CS.DeploymentController.Instance:AddAndPlayPerformance(CheckResult);
end

local CheckBattle = function(self)
	local spotAction = CS.GameData.engagedSpot;
	if CS.GameData.missionResult == nil and CS.GameData.enemyOtherEngagedSpot == nil and spotAction ~= nil then
		if spotAction.layer == CS.DeploymentBackgroundController.currentlayer then
			if spotAction.spot.currentTeamTemp == nil and self._randomEventController ~= nil and self._randomEventController.gameObject.activeSelf then
				self:GoBattle();
				return;
			end
		end
	end
	if CS.GameData.missionResult ~= nil then
		CS.GameData.missionAction.queuePerformanceHandler:Clear();
	end
	self:CheckBattle();
end

local FinishMissionEvent = function()
	CS.DeploymentController.TriggerFinishMissionEvent();
end
local RequestAbortMissionHandle = function(self,www)
	CS.Data.DelKeyFromPlayerPref("PointAVG");
	self:AddAndPlayPerformance(nil);
	local hasResultUI = false;
	local jsonData = CS.ConnectionController.DecodeAndMapJson(www.text);
	local checklose = CS.GameData.AnalysisMissionResult(jsonData, false);
	if checklose then
		CS.UnityEngine.PlayerPrefs.SetInt("MissonResult", 0);
		CS.GameData.missionAction:EmptyMreAmmo();
		local jsonResult = jsonData:GetValue("mission_lose_result");
		if jsonResult:Contains("guns_in_coinMission") then
			local jsonGunsInMission = jsonResult:GetValue("guns_in_coinMission");
			for i=0,jsonGunsInMission.Count-1 do
				local gunid = jsonGunsInMission[i]:GetValue("id").Long;
				local life = jsonGunsInMission[i]:GetValue("life").Int;
				local gun = CS.GameData.listGun:GetDataById(gunid);
				if gun ~= nil then
					gun.life = life;
				end
			end
		end
		if CS.GameData.currentSelectedMissionInfo.isEndless then
			hasResultUI = true;
			self:AddAndPlayPerformance(FinishMissionEvent);
		else
			CS.GameData.ClearMissionActionData();
			CS.GF.Battle.SkillUtils.ClearSkillCD();
		end	
	else
		local checkwin = CS.GameData.AnalysisMissionResult(jsonData, true);
		if checkwin then
			CS.UnityEngine.PlayerPrefs.SetInt("MissonResult", 1);
			hasResultUI = true;
			self:AddAndPlayPerformance(FinishMissionEvent);
		end
	end
	if self.restart then
		CS.CommonController.GotoScene("Deployment");
	elseif not hasResultUI then
		if CS.GameData.currentSelectedMissionInfo.missionType == CS.MissionType.simulation then
			CS.CommonController.GotoScene("MissionSelection", 2, CS.GameData.currentSelectedMissionInfo.duplicateType);
		else
			CS.OPSConfig.Instance:GoToScene(CS.GameData.currentSelectedMissionInfo.campaign);
		end	
	end		
end

local CheckAllySpotAction = function()
	CS.DeploymentController.Instance:CheckAllySpotAction();
end
local CheckBuildCastSkillOnDeath = function()
	CS.DeploymentController.Instance:CheckBuildCastSkillOnDeath();
end
local RequestNoBattleAllyHandle = function(self,data)
	local checklose = CS.GameData.AnalysisMissionResult(data.jsonData, false);
	if not checklose then
		local checkwin = CS.GameData.AnalysisMissionResult(data.jsonData, true);
	end
	self:AddInsertPlayPerfomance(CheckAllySpotAction);
	self:AddInsertPlayPerfomance(CheckBuildCastSkillOnDeath);
	self:AddAndPlayPerformance(nil);
end

local CheckEvent = function()
	if CS.GameData.missionAction ~= nil and CS.GameData.missionAction.queuePerformanceHandler.Count ~= 0 then
		return;
	end
	if CS.DeploymentController.CanPlayerClickEvent ~= nil then
		CS.DeploymentController.CanPlayerClickEvent();
		CS.DeploymentController.CanPlayerClickEvent = nil;
	end
end

local TriggerCanPlayerClickEvent = function()
	CS.DeploymentController.AddAction(CheckEvent,0.3);
end

local AnalysisNightEnemy = function(self,data,playEnemyMove)
	self:AnalysisNightEnemy(data,playEnemyMove);
	for i=0,CS.DeploymentBackgroundController.Instance.listSpot.Count-1 do
		local spot = CS.DeploymentBackgroundController.Instance.listSpot[i];
		if spot.currentTeam ~= nil and not spot.currentTeam:isNull() and spot.currentTeamTemp ~= nil and not spot.currentTeamTemp:isNull() then
			if spot.currentTeam.teamId == spot.currentTeamTemp.teamId then
				spot.currentTeamTemp:Hide();
			end
		end
	end
end

local TriggerMoveCameraEvent = function(target,move,recordPos,changescale,setscale,handle)
	if CS.DeploymentTeamController.transferSpeed > 1 then
		if CS.GameData.missionAction ~= nil and CS.GameData.missionAction.transTeamDatas.Count > 0 then
			local pos = CS.DeploymentBackgroundController.currentLayerData.offset;
			CS.DeploymentController.TriggerMoveCameraEvent(pos,true,true,true,0.26,nil);
			return;
		end
	end
	CS.DeploymentController.TriggerMoveCameraEvent(target,move,recordPos,changescale,setscale,handle);
end

local GoToBattleScene = function(self)
	if not self.engagedSpot.hasEnemyTeam and not self.engagedSpot.hasOtherTeam then
		self.engagedSpot = nil;
		self:CheckBattle();
		return;
	end
	if self.engagedSpot.enemyInstanceId ~= 0 then
		local enemyTeam = CS.GameData.missionAction.listEnemyTeams:GetDataById(self.engagedSpot.enemyInstanceId);
		if enemyTeam.hpPercent == 0 and enemyTeam.bossHp > 0 then
			enemyTeam.hpPercent = 0.1;
		end
	end
	self:GoToBattleScene();
end

local CheckTeamCanMove = function(self,spot)
	if self.currentSelectedTeam ~= nil and self.currentSelectedTeam.currentCanNotMove then
		return false;
	end
	return self:CheckTeamCanMove(spot);
end
local CheckTeamBothCanMove = function(self,spot)
	if self.currentSelectedTeam.currentCanNotMove then
		return false;
	end
	if spot.currentTeam ~= nil and spot.currentTeam:CurrentTeamBelong() == CS.TeamBelong.friendly then			
		if spot.currentTeam.currentCanNotMove then
			return false;
		end
	end
				
	return self:CheckTeamBothCanMove(spot);
end
local PlayGrowSummonEnemy = function(self)
	for i=0,CS.GameData.missionAction.growSpots.Count-1 do
		local spotAction = CS.GameData.missionAction.growSpots[i];
		if spotAction.enemyInstanceId ~= 0 then
			if spotAction.spot.currentTeam ~= nil and spotAction.spot.currentTeam.enemyInstanceId ~= nil and spotAction.spot.currentTeam.enemyInstanceId ~= spotAction.enemyInstanceId then
				spotAction.spot.currentTeam:Hide();
				spotAction.spot.currentTeam = nil;
			end 
		end
		if spotAction.allyTeamInstanceIds.Count>0 then
			if spotAction.spot.currentTeam ~= nil and spotAction.spot.currentTeam.allyTeamInstanceId~= nil and spotAction.allyTeamInstanceIds:Contains(spotAction.spot.currentTeam.allyTeamInstanceId) then
				spotAction.spot.currentTeam:Hide();
				spotAction.spot.currentTeam = nil;
			end 
		end
	end
	self:PlayGrowSummonEnemy();
end

local PlaySpotTeamCapture = function(self)
	playSpotTeamCapture = 0;
	for i=0,self.cannotPlayLayer.Count-1 do
		for j=CS.GameData.missionAction.queueSpotTeamCapture.Count-1,0,-1 do
			local record = CS.GameData.missionAction.queueSpotTeamCapture[j];
			if record.spotAction.layer == self.cannotPlayLayer[i] then
				record.spotAction.spot:PlayCaptureRecord(record, true, false);
				CS.GameData.missionAction.queueSpotTeamCapture:RemoveAt(j);
			end
		end
	end
	playSpotTeamCapture = 1;
	self:PlaySpotTeamCapture();
end

local PlaySpotSurroundCapture = function(self)
	playSpotTeamCapture = 2;
	self:PlaySpotSurroundCapture();
end
local CheckPlayerLayers = function(self)
	self:CheckPlayerLayers();
	for j=CS.GameData.missionAction.queueSpotTeamCapture.Count-1,0,-1 do
		local record = CS.GameData.missionAction.queueSpotTeamCapture[j];
		if not CS.DeploymentBackgroundController.playlayers:Contains(record.spotAction.layer) then
			record.spotAction.spot:PlayCaptureRecord(record, true, false);
			CS.GameData.missionAction.queueSpotTeamCapture:RemoveAt(j);
		end
	end	
end

local TriggerSwitchAbovePanelEvent = function(show)
	if CS.DeploymentController.Instance ~= nil then
		if CS.DeploymentController.Instance.engagedSpot ~= nil then
			CS.DeploymentController.TriggerSwitchAbovePanelEvent(true);
			return;
		end
	end
	CS.DeploymentController.TriggerSwitchAbovePanelEvent(show);
end

local triggerGuide = function()
	CS.GuideDeploymentController.Instance:TriggerGuide(CS.TriggerDeploymentCondition.StartMission);
end
local RequestStartMissionHandle = function(self,www)
	self:RequestStartMissionHandle(www);
	self:AddAndPlayPerformance(triggerGuide);
end

local CheckTeam = function(self,teamController,delay)
	self:CheckTeam(teamController,delay);
	if teamController.currentSpot.currentTeamTemp == teamController then
		if teamController.allyTeam ~= nil and teamController.allyTeam.isCuiPi then
			teamController.currentSpot.currentTeamTemp = teamController.currentSpot.currentTeam;
		end
	end	
end

local TriggerSelectSpot = function(spot)
	if spot.currentTeam ~= nil and CS.DeploymentPlanModeController.Instance.status == CS.DeploymentPlanModeController.PlanStatus.pause then
		CS.DeploymentPlanModeController.Instance.status = CS.DeploymentPlanModeController.PlanStatus.wait;
	end
	CS.DeploymentController.TriggerSelectSpot(spot);
end
function HasCanControlTeam()
	for i=0,CS.DeploymentController.Instance.playerTeams.Count-1 do
		if CS.DeploymentController.Instance.playerTeams[i]:CanPlayerHandControl() then
			return true;
		end
	end
	for i=0,CS.DeploymentController.Instance.allyTeams.Count-1 do
		if CS.DeploymentController.Instance.allyTeams[i]:CanPlayerHandControl() then
			return true;
		end
	end
	for i=0,CS.DeploymentController.Instance.sangvisTeams.Count-1 do
		if CS.DeploymentController.Instance.sangvisTeams[i]:CanPlayerHandControl() then
			return true;
		end
	end
	for i=0,CS.DeploymentController.Instance.squadTeams.Count-1 do
		if CS.DeploymentController.Instance.squadTeams[i]:CanPlayerHandControl() then
			return true;
		end
	end
	return false;  
end
function HasDeploySpot()
	for i=0,CS.DeploymentBackgroundController.Instance.listSpot.Count-1 do
		local spot = CS.DeploymentBackgroundController.Instance.listSpot:GetDataByIndex(i);
		if CS.DeploymentController.CanDeploy(spot) then
			return true;
		end
	end
	return false;
end
local RequestStartTurnHandle = function(self,www)
	local spot = CS.SpotInfo();
	spot.id = -1;
	spot.type = CS.SpotType.headQuarter;
	spot.belong = CS.Belong.friendly;
	if HasCanControlTeam() or HasDeploySpot() then
		CS.DeploymentBackgroundController.Instance.listSpotInfo:Add(spot);
	end
	self:RequestStartTurnHandle(www);
	CS.DeploymentBackgroundController.Instance.listSpotInfo:Remove(spot);
end

local check = false;
local CanPlayerAction = function(self)
	if check then
		return true;
	end
	if CS.GameData.currentSelectedMissionInfo.useDemoMission then
		return false;	
	end
	return true;
end

local ClickSpot = function(self,spot)
	check = true;
	self:ClickSpot(spot);
	check = false;
end

local Awake = function(self)
	if CS.GameData.missionAction == nil then
		CS.GameData.missionResult = nil;
	end
	self:Awake();
end

local CreateTeam = function(self,selectedSpot,teamId,teamType,grow,growtype)
	if selectedSpot.packageIgnore then
		return;
	end
	self:CreateTeam(selectedSpot,teamId,teamType,grow,growtype);
end

util.hotfix_ex(CS.DeploymentController,'BuildCastSkillOnDeathHandler',BuildCastSkillOnDeathHandler)
util.hotfix_ex(CS.DeploymentController,'InitTeamSpots',InitTeamSpots)
util.hotfix_ex(CS.DeploymentController,'CheckBattle',CheckBattle)
util.hotfix_ex(CS.DeploymentController,'RequestAbortMissionHandle',RequestAbortMissionHandle)
util.hotfix_ex(CS.DeploymentController,'RequestNoBattleAllyHandle',RequestNoBattleAllyHandle)
util.hotfix_ex(CS.DeploymentController,'TriggerCanPlayerClickEvent',TriggerCanPlayerClickEvent)
util.hotfix_ex(CS.DeploymentController,'AnalysisNightEnemy',AnalysisNightEnemy)
util.hotfix_ex(CS.DeploymentController,'TriggerMoveCameraEvent',TriggerMoveCameraEvent)
util.hotfix_ex(CS.DeploymentController,'GoToBattleScene',GoToBattleScene)
util.hotfix_ex(CS.DeploymentController,'CheckTeamCanMove',CheckTeamCanMove)
util.hotfix_ex(CS.DeploymentController,'CheckTeamBothCanMove',CheckTeamBothCanMove)
util.hotfix_ex(CS.DeploymentController,'PlayGrowSummonEnemy',PlayGrowSummonEnemy)
util.hotfix_ex(CS.DeploymentController,'PlaySpotTeamCapture',PlaySpotTeamCapture)
util.hotfix_ex(CS.DeploymentController,'PlaySpotSurroundCapture',PlaySpotSurroundCapture)
util.hotfix_ex(CS.DeploymentController,'CheckPlayerLayers',CheckPlayerLayers)
util.hotfix_ex(CS.DeploymentController,'TriggerSwitchAbovePanelEvent',TriggerSwitchAbovePanelEvent)
util.hotfix_ex(CS.DeploymentController,'CheckTeam',CheckTeam)
util.hotfix_ex(CS.DeploymentController,'TriggerSelectSpot',TriggerSelectSpot)
util.hotfix_ex(CS.DeploymentController,'RequestStartTurnHandle',RequestStartTurnHandle)
util.hotfix_ex(CS.DeploymentController,'get_CanPlayerAction',CanPlayerAction)
util.hotfix_ex(CS.DeploymentController,'Awake',Awake)
util.hotfix_ex(CS.DeploymentController,'CreateTeam',CreateTeam)
util.hotfix_ex(CS.DeploymentController,'ClickSpot',ClickSpot)


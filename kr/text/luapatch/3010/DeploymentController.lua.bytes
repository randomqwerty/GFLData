local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentController)
playteams = nil;
playbuilds = nil;
--补上设施状态刷新人物UI刷新
local CheckBuild = function()
	--CS.DeploymentController.TriggerRefreshUIEvent();
	if playbuilds ~= nil then
		for i=0,playbuilds.Count -1 do
			playbuilds[i]:RefreshController();
		end
	end
	if playteams ~= nil then
		for i=0,playteams.Count -1 do
			playteams[i]:RefreshTeamInfo();
		end
	end
	CS.DeploymentController.Instance:ViewSummary();
	CS.DeploymentUIController.Instance:RefreshUI();
	CS.DeploymentController.Instance:AddAndPlayPerformance(nil);
end

local CheckAllyDie = function()
	CS.DeploymentController.Instance:CheckAllyTeamAutoDie();
end
local checkUI = false;
--修正设施延迟刷新
local RequestStartTurnHandle = function(self,json)
	if playteams == nil then
		playteams = CS.System.Collections.Generic.List(CS.DeploymentTeamController)();
	end
	playteams:Clear();
	for i=0,self.playerTeams.Count-1 do
		playteams:Add(self.playerTeams[i]);
	end
	for i=0,self.enemyTeams.Count-1 do
		playteams:Add(self.enemyTeams[i]);
	end
	for i=0,self.squadTeams.Count-1 do
		playteams:Add(self.squadTeams[i]);
	end
	for i=0,self.allyTeams.Count-1 do
		playteams:Add(self.allyTeams[i]);
	end
	for i=0,self.sangvisTeams.Count-1 do
		playteams:Add(self.sangvisTeams[i]);	
	end
	if playbuilds == nil then
		playbuilds = CS.System.Collections.Generic.List(CS.DeploymentBuildingController)();	
	end
	playbuilds:Clear();
	local builds = {};
	for i=0,CS.DeploymentBackgroundController.Instance.listBuildingController.Count -1 do
		local build = CS.DeploymentBackgroundController.Instance.listBuildingController[i];
		playbuilds:Add(build);
		table.insert(builds,build);
	end
	CS.DeploymentBackgroundController.Instance.listBuildingController:Clear();
	checkUI = true;
	self:AddAndPlayPerformance(CheckAllyDie);
	self:RequestStartTurnHandle(json);
	for i=1,#builds do
		CS.DeploymentBackgroundController.Instance.listBuildingController:Add(builds[i]);
	end
	checkUI = false;
	self:AddAndPlayPerformance(CheckBuild);
end

local PlayView = function()
	CS.DeploymentController.Instance:PlayViewSummary();
end

local CheckLayerFinal = function()
	local layer = CS.DeploymentBackgroundController.Instance.currentUILayer;
	CS.DeploymentBackgroundController.currentlayer = layer;
	CS.DeploymentBackgroundController.Instance:SwitchLayer(layer, PlayView, false);
end
--修正设施延迟刷新
local AddAllCanPlayPerformanceLayer = function(self)
	local builds = {};
	for i=0,CS.DeploymentBackgroundController.Instance.listBuildingController.Count -1 do
		local build = CS.DeploymentBackgroundController.Instance.listBuildingController[i];
		table.insert(builds,build);
	end
	CS.DeploymentBackgroundController.Instance.listBuildingController:Clear();
	self:AddAllCanPlayPerformanceLayer();
	for i=1,#builds do
		CS.DeploymentBackgroundController.Instance.listBuildingController:Add(builds[i]);
	end
	while CS.GameData.missionAction.queuePerformanceHandler.Count > 1 do
		CS.DeploymentController.savePlayQueue:Enqueue(CS.GameData.missionAction.queuePerformanceHandler:Dequeue())
	end
	CS.GameData.missionAction.queuePerformanceHandler:Clear();
	while CS.DeploymentController.savePlayQueue.Count > 0 do
		CS.GameData.missionAction.queuePerformanceHandler:Enqueue(CS.DeploymentController.savePlayQueue:Dequeue())
	end
	self:AddAndPlayPerformance(CheckLayerFinal);
end

local spotid = 0;

local CheckSpot = function()
	local spot = CS.DeploymentBackgroundController.Instance.listSpot:GetDataById(spotid);
	if spot ~= nil and spot.currentTeam == nil and spot.currentTeamTemp ~= nil then
		spot.currentTeam = spot.currentTeamTemp;
		spot.currentTeamTemp = nil;
	end
end

local PlayShowAllTeamForce = function(self,changeData,play)
	self:PlayShowAllTeamForce(changeData,play);
	spotid = changeData.changeData:GetValue("spot_id").Int;
	CS.DeploymentController.AddAction(CheckSpot,2.2);
end
--修正整体UI层级
local InitUIElements = function(self)
	self:InitUIElements();
	self.holderInfo:GetComponent(typeof(CS.UnityEngine.Canvas)).sortingOrder = 2;
	self.uiInfo:GetComponent(typeof(CS.UnityEngine.Canvas)).sortingOrder = 4;
	self.spotInfo:GetComponent(typeof(CS.UnityEngine.Canvas)).sortingOrder = 1;	
	self.OptionInfo:GetComponent(typeof(CS.UnityEngine.Canvas)).sortingOrder = 3;	
end

local TriggerSelectTeam = function(team)
	if team ~= nil then
		if team.currentSpot.currentTeam ~= team then
			CS.DeploymentController.TriggerSelectTeam(nil);
			return;
		end
	end
	CS.DeploymentController.TriggerSelectTeam(team);
end
function ShowSettlement()
	if CS.GameData.currentSelectedMissionInfo.missionType ~= CS.MissionType.simulation then
		CS.DeploymentController.Instance:ShowCommonBattleSettlement();
	else
		CS.DeploymentController.Instance:ShowSimulationSettlement();
	end
end
local ShowSettlement = function(self)
	self:AddAndPlayPerformance(ShowSettlement);
	self:AddAndPlayPerformance(nil);
end

local TriggerRefreshUIEvent = function()
	if checkUI then
		return;
	end
	CS.DeploymentController.TriggerRefreshUIEvent();
end

local SelectTeamSelf = function()
	CS.DeploymentController.TriggerSelectTeam(CS.DeploymentController.Instance.currentSelectedTeam);
end
local ViewSummary = function()
	CS.DeploymentController.Instance:PlayViewSummary();
end
local RequestMoveTeamHandle = function(self,request)
	self:RequestMoveTeamHandle(request);
	if self._randomEventController == nil then
		self:AddAndPlayPerformance(ViewSummary);
		self:AddAndPlayPerformance(0.2,SelectTeamSelf,true);
	end
end

local SelectTeam = function(self,team)
	if team ~= nil then
		CS.CommonAudioController.PlayUI(CS.AudioUI.UI_selete);
		CS.DeploymentController.lastSelectedTeamID = team.teamId;
		CS.DeploymentController.TriggerCrossMoveEvent(team.currentSpot.gameObject);
	else
		CS.DeploymentController.TriggerCrossMoveEvent(nil);
	end
	self.currentSelectedTeam = team;
end
local InitField = function(self)
	self:InitField();
	CS.DeploymentUIController.Instance.showall = true;
end

local CheckAbove = function()
	CS.DeploymentController.TriggerSwitchAbovePanelEvent(false);
end

local CheckNext = function(self)
	self:CheckNext();
	if CS.GameData.missionAction.currentTurnBelong == CS.MissionAction.TurnBelong.SelfTurn then
		CS.DeploymentController.AddAction(CheckAbove,4);
	end
end
util.hotfix_ex(CS.DeploymentController,'InitUIElements',InitUIElements)
util.hotfix_ex(CS.DeploymentController,'RequestStartTurnHandle',RequestStartTurnHandle)
util.hotfix_ex(CS.DeploymentController,'AddAllCanPlayPerformanceLayer',AddAllCanPlayPerformanceLayer)
util.hotfix_ex(CS.DeploymentController,'PlayShowAllTeamForce',PlayShowAllTeamForce)
util.hotfix_ex(CS.DeploymentController,'TriggerSelectTeam',TriggerSelectTeam)
util.hotfix_ex(CS.DeploymentController,'ShowSettlement',ShowSettlement)
util.hotfix_ex(CS.DeploymentController,'TriggerRefreshUIEvent',TriggerRefreshUIEvent)
util.hotfix_ex(CS.DeploymentController,'RequestMoveTeamHandle',RequestMoveTeamHandle)
util.hotfix_ex(CS.DeploymentController,'SelectTeam',SelectTeam)
util.hotfix_ex(CS.DeploymentController,'InitField',InitField)
util.hotfix_ex(CS.DeploymentController,'CheckNext',CheckNext)




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
	self:RequestStartTurnHandle(json);
	for i=1,#builds do
		CS.DeploymentBackgroundController.Instance.listBuildingController:Add(builds[i]);
	end
	checkUI = false;
	self:AddAndPlayPerformance(CheckBuild);
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
	CS.DeploymentController.AddAction(SelectTeamSelf,0.2);
end
local RequestMoveTeamHandle = function(self,request)
	self:RequestMoveTeamHandle(request);
	self:AddAndPlayPerformance(ViewSummary);
end

local CheckBuildActionSkill = function(self,team,buildskill)
	self:CheckBuildActionSkill(team,buildskill);
	for i=0,buildskill.Count-1 do
		for j=buildskill[i].targetSpotAction.Count-1,0,-1 do
			local spot = buildskill[i].targetSpotAction[j].spot;
			if not spot.Show then
				buildskill[i].targetSpotAction:RemoveAt(j);
			end
		end
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
util.hotfix_ex(CS.DeploymentController,'CheckBuildActionSkill',CheckBuildActionSkill)



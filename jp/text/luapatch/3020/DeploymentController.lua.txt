local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentController)

local InitStartTurnAllLayerPlays = function(self,onlyCheckMove)
	if onlyCheckMove then
		if CS.GameData.missionAction.queuePerformanceHandler.Count == 0 then
			self.isPlayingPerformance = false;
		end
	end
	self:InitStartTurnAllLayerPlays(onlyCheckMove);
end

local CheckBattle = function()
	CS.DeploymentController.Instance:CheckBattle();
end
local AddCheckBattle = function()
	CS.DeploymentController.Instance:AddAndPlayPerformance(CheckBattle);
end
local BuildCastSkillOnDeathHandler = function(self,data)
	self:BuildCastSkillOnDeathHandler(data);
	self:InsertSomePlayPerformances(AddCheckBattle);
end
local RequestStartMissionHandle = function(self,json)
	for i=0,CS.DeploymentBackgroundController.Instance.listSpot.Count-1 do
		local spot = CS.DeploymentBackgroundController.Instance.listSpot[i];
		local spotaction = CS.GameData.listSpotAction:GetDataById(spot.spotInfo.id);
		if spotaction ~= nil then
			if spotaction.allyTeamInstanceIds.Count>0 then
				local instanceId = spotaction.allyTeamInstanceIds[0];
				if spot.currentTeam ~= nil then
					spot.currentTeam.allyTeam = CS.GameData.missionAction.listAllyTeams:GetDataById(instanceId);
				end
			end
		end
	end
	self:RequestStartMissionHandle(json);
	CS.GameData.missionAction:LoadAvgData(json);
	self:AddPlayMissionTriggerAvg();
end

local TriggerSwitchAbovePanelEvent = function(show)
	if CS.DeploymentController.Instance ~= nil and not CS.DeploymentController.Instance:isNull() then
		if not show then
			if CS.GameData.missionAction ~= nil and CS.GameData.missionAction.queuePerformanceHandler.Count == 0 then
				CS.DeploymentController.Instance.isPlayingPerformance = false;
			end
		end
	end
	CS.DeploymentController.TriggerSwitchAbovePanelEvent(show);
end

local myCheckAction = function(self)
	local eventSystem = CS.UnityEngine.GameObject.Find("EventSystem"):GetComponent(typeof(CS.UnityEngine.EventSystems.EventSystem));
	print(eventSystem:ToString());
	self:CheckAction();
end

local InitTeamSpots = function(self)
	if CS.UnityEngine.GameObject.Find("/Reporter") ~= nil then
		CS.NDebug.PrintLog = true;
		CS.UnityEngine.Debug.unityLogger.logEnabled = true;
	end
	self:InitTeamSpots();
end

local CheckFriendAllyTeamTurnEvent = function()
	if CS.DeploymentController.Instance ~= nil then
		CS.DeploymentController.Instance:RequestFriendAllyTeamTurn();
	end
end 
local TriggerFriendAllyTeamTurnEvent = function()
	CS.DeploymentPlanModeController.Instance.enabled = true;
	CS.DeploymentController.AddAction(CheckFriendAllyTeamTurnEvent,0.1);
end

local cantransfer = function(skill,spot)
	if spot.spotAction.isRandom then
		return false;
	end
	if spot.CanNotEnter then
		return false;
	end
	if skill.is_airborne == 2 then
		for i=0,spot.spotAction.listSpecialAction.Count-1 do
			local specialAction = spot.spotAction.listSpecialAction[i];
			if specialAction.spotBuffInfo ~= nil and specialAction.spotBuffInfo.noairborne then
				return false;
			end
		end
	end
	return true;
end

local ClickAllyTeam = function(self,allyteamController)
	if CS.DeploymentController.isDeplyment then
		if not allyteamController.isFriend then
			return;
		end
	end
	self:ClickAllyTeam(allyteamController);
end

local CheckNext = function(self)
	local check = CS.DeploymentController.firestCheck;
	if CS.GameData.currentSelectedMissionInfo.specialType == CS.MapSpecialType.Night then
		CS.DeploymentController.firestCheck = false;
	end
	self:CheckNext();
	if check and CS.GameData.currentSelectedMissionInfo.specialType == CS.MapSpecialType.Night then
		if CS.GameData.missionAction.currentTurnBelong == CS.MissionAction.TurnBelong.FriendTurn then
			self:AddAndPlayPerformance(function()
				CS.DeploymentController.TriggerFriendTurnEvent();
			end)
		elseif CS.GameData.missionAction.currentTurnBelong == CS.MissionAction.TurnBelong.FriendAllyTurn then
			self:AddAndPlayPerformance(function()
					CS.DeploymentController.TriggerFriendAllyTeamTurnEvent();
				end)
		elseif CS.GameData.missionAction.currentTurnBelong == CS.MissionAction.TurnBelong.EnemyTurnStart then
			self:AddAndPlayPerformance(function()
					CS.DeploymentController.TriggerEnemyTurnMoveEvent();
				end)
		elseif CS.GameData.missionAction.currentTurnBelong == CS.MissionAction.TurnBelong.EnemyTurnEnd then
			self:AddAndPlayPerformance(function()
					CS.DeploymentController.TriggerStartThirdTurnEvent();
				end)
		elseif CS.GameData.missionAction.currentTurnBelong == CS.MissionAction.TurnBelong.ThirdTurnStart then
			self:AddAndPlayPerformance(function()
					CS.DeploymentController.TriggerOthersideTurnMoveEvent();
				end)
		elseif CS.GameData.missionAction.currentTurnBelong == CS.MissionAction.TurnBelong.ThirdTurnEnd then
			self:AddAndPlayPerformance(function()
					CS.DeploymentController.TriggerStartTurnEvent();
				end)
		end
	end
end

local SangvisTeamsCount = function(self)
	local num = 0;
	for i=0,self.sangvisTeams.Count-1 do
		local team = self.sangvisTeams[i];
		if team ~= nil and team.teamId > 0 then
			num = num + 1;
		end
	end
	return num;
end
local TriggerAbortMissionEvent = function()
	if CS.GameData.missionAction == nil then
		return;
	end
	if CS.DeploymentController.Instance ~= nil then
		CS.DeploymentController.Instance:RequestAbortMission();
	end
end
local CheckOnePoint = function(self)
	if CS.GameData.engagedSpot ~= nil then
		return;
	end
	self:CheckOnePoint();
end
local CheckDeploymentNotice = function(self)
	self:CheckDeploymentNotice();
	self:ViewSummary();
end
local CheckTeamTrans = function(self)
	if CS.GameData.missionAction.transTeamDatas.Count == 0 then
		self:AddAndPlayPerformance(nil);
		return;
	end
	self:CheckTeamTrans();
end
util.hotfix_ex(CS.DeploymentController,'InitStartTurnAllLayerPlays',InitStartTurnAllLayerPlays)
util.hotfix_ex(CS.DeploymentController,'BuildCastSkillOnDeathHandler',BuildCastSkillOnDeathHandler)
--util.hotfix_ex(CS.DeploymentController,'AddAllCanPlayPerformanceLayer',AddAllCanPlayPerformanceLayer)
util.hotfix_ex(CS.DeploymentController,'RequestStartMissionHandle',RequestStartMissionHandle)
util.hotfix_ex(CS.DeploymentController,'TriggerSwitchAbovePanelEvent',TriggerSwitchAbovePanelEvent)
util.hotfix_ex(CS.DeploymentController,'InitTeamSpots',InitTeamSpots)
util.hotfix_ex(CS.DeploymentController,'TriggerFriendAllyTeamTurnEvent',TriggerFriendAllyTeamTurnEvent)
util.hotfix_ex(CS.DeploymentController,'cantransfer',cantransfer)
util.hotfix_ex(CS.DeploymentController,'ClickAllyTeam',ClickAllyTeam)
util.hotfix_ex(CS.DeploymentController,'CheckNext',CheckNext)
util.hotfix_ex(CS.DeploymentController,'get_SangvisTeamsCount',SangvisTeamsCount)
util.hotfix_ex(CS.DeploymentController,'TriggerAbortMissionEvent',TriggerAbortMissionEvent)
util.hotfix_ex(CS.DeploymentController,'CheckOnePoint',CheckOnePoint)
util.hotfix_ex(CS.DeploymentController,'CheckDeploymentNotice',CheckDeploymentNotice)
util.hotfix_ex(CS.DeploymentController,'CheckTeamTrans',CheckTeamTrans)
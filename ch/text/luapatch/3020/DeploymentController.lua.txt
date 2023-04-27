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
	if spot.spotAction.HasTeam then
		return false;
	end
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
util.hotfix_ex(CS.DeploymentController,'InitStartTurnAllLayerPlays',InitStartTurnAllLayerPlays)
util.hotfix_ex(CS.DeploymentController,'BuildCastSkillOnDeathHandler',BuildCastSkillOnDeathHandler)
--util.hotfix_ex(CS.DeploymentController,'AddAllCanPlayPerformanceLayer',AddAllCanPlayPerformanceLayer)
util.hotfix_ex(CS.DeploymentController,'RequestStartMissionHandle',RequestStartMissionHandle)
util.hotfix_ex(CS.DeploymentController,'TriggerSwitchAbovePanelEvent',TriggerSwitchAbovePanelEvent)
util.hotfix_ex(CS.DeploymentController,'InitTeamSpots',InitTeamSpots)
util.hotfix_ex(CS.DeploymentController,'TriggerFriendAllyTeamTurnEvent',TriggerFriendAllyTeamTurnEvent)
util.hotfix_ex(CS.DeploymentController,'cantransfer',cantransfer)
util.hotfix_ex(CS.DeploymentController,'ClickAllyTeam',ClickAllyTeam)

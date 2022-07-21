local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentController)

local RequestNoBattleAllyHandle = function(self,data)
	local json = data.jsonData:GetValue("life_change");
	local keys = CS.System.Collections.Generic.List(CS.System.String)(json.Keys);
	for i=0,keys.Count-1 do
		local temp = json:GetValue(keys[i]);
		if temp:Contains("enemy_hp_percent") then
			local hp = temp:GetValue("enemy_hp_percent").Float;
			local spotid = tonumber(keys[i]);
			local spotaction = CS.GameData.listSpotAction:GetDataById(spotid);
			for j = 0, spotaction.allyTeamInstanceIds.Count-1 do
				local allyteam = CS.GameData.missionAction.listAllyTeams:GetDataById(spotaction.allyTeamInstanceIds[j]);
				allyteam.hpPercent = hp;
			end
		end
	end
	self:RequestNoBattleAllyHandle(data);
end

local TriggerSelectTeam = function(team)
	if team == nil then
		CS.DeploymentBuildSkillItem.showSelectSpot = false;
	end
	CS.DeploymentController.TriggerSelectTeam(team);
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

local PlayShowAllTeamForce = function(self,changeData,play)
	self:PlayShowAllTeamForce(changeData,play);
	if changeData.type == 0 then
		local instanceId = changeData.changeData:GetValue("ally_instance_id").Long;
		local allTeam = CS.GameData.missionAction.listAllyTeams:GetDataById(instanceId);
		if allTeam.allyTeamController ~= nil then
			allTeam.allyTeamController.mRecordItem:Clear();
			allTeam.allyTeamController:AnalysicsDropData();
		end
	end
end

local RequestEndEnemyTurnHandle = function(self,data)
	self:RequestEndEnemyTurnHandle(data);
	if CS.GameData.missionAction.queuePerformanceHandler.Count > 0 and self.isPlayingPerformance then
		self:AddAndPlayPerformance(nil);
	end
end

local CheckControlUI = function(self,teamcontroller)
	local skills = self:CheckControlUI(teamcontroller);
	for i=0,skills.Count-1 do
		local skill = skills[i];
		for j=skill.otherskills.Count-1,0,-1 do
			if skill.otherskills[j].playerControl then
				skill.otherskills:RemoveAt(j);
			end
		end
	end
	return skills;
end

local EndTurnPlayAllData= function(self)
	self.isPlayingPerformance = false;
	self:EndTurnPlayAllData();
end

local GoToBattleScene = function(self)
	if self.engagedSpot.enemyInstanceId ~= 0 then
		local enemyTeam = CS.GameData.missionAction.listEnemyTeams:GetDataById(self.engagedSpot.enemyInstanceId);
		if enemyTeam.hpPercent< 0.01 then
			enemyTeam.hpPercent = 0.01;
		end
		print("修改修小血量"..enemyTeam.hpPercent)
	end
	if self.engagedSpot.allyTeamInstanceIds.Count > 0 then
		for i=0,self.engagedSpot.allyTeamInstanceIds.Count-1 do
			local ally = CS.GameData.missionAction.listAllyTeams:GetDataById(self.engagedSpot.allyTeamInstanceIds[i]);
			if ally.hpPercent< 0.01 then
				ally.hpPercent = 0.01;
			end
			print("修改修小血量"..ally.hpPercent)
		end
	end
	self:GoToBattleScene();
end
local RequestStartThirdAllyTeamTurnHandle = function(self,data)
	self:RequestStartThirdAllyTeamTurnHandle(data);
	CheckGrowEnemySpot(self);
end
local RequestStartEnemyTurnHandle = function(self,data)
	self:RequestStartEnemyTurnHandle(data);
	CheckGrowEnemySpot(self);
end
function CheckGrowEnemySpot(self)
	for i=0,self.growEnemySpot.Count-1 do
		local spot = self.growEnemySpot[i];
		if spot.spotAction.allyTeamInstanceIds.Count == 2 then
			if spot.spotAction.allyTeamInstanceIds[0]==spot.spotAction.allyTeamInstanceIds[1] then
				spot.spotAction.allyTeamInstanceIds:RemoveAt(0);
			end
		end
	end
	while self.growEnemySpot.Count>0 do
		local spot = self.growEnemySpot[0];
		self.growEnemySpot:Remove(spot);
		local play = spot.layer == CS.DeploymentBackgroundController.currentlayer;
		if spot.spotAction.enemyInstanceId ~= 0 then
			local enemy = CS.GameData.missionAction.listEnemyTeams:GetDataById(spot.spotAction.enemyInstanceId);
			enemy.hpPercent = 1;
			self:CreateTeam(spot, 0, CS.DeploymentController.TeamType.enemyTeam, play);
		elseif spot.spotAction.allyTeamInstanceIds.Count > 0 then
			self:CreateTeam(spot, 0, CS.DeploymentController.TeamType.allyTeam, play);	
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

local CheckUIOneLayer = function(self)
	self:CheckUIOneLayer();
	CS.GameData.missionAction.queueSpotTeamCapture:Clear();
	CS.GameData.missionAction.queueSpotSurroundCapture:Clear();
end
util.hotfix_ex(CS.DeploymentController,'RequestNoBattleAllyHandle',RequestNoBattleAllyHandle)
util.hotfix_ex(CS.DeploymentController,'TriggerSelectTeam',TriggerSelectTeam)
util.hotfix_ex(CS.DeploymentController,'get_CanPlayerAction',CanPlayerAction)
util.hotfix_ex(CS.DeploymentController,'ClickSpot',ClickSpot)
util.hotfix_ex(CS.DeploymentController,'PlayShowAllTeamForce',PlayShowAllTeamForce)
--util.hotfix_ex(CS.DeploymentController,'RequestEndEnemyTurnHandle',RequestEndEnemyTurnHandle)
util.hotfix_ex(CS.DeploymentController,'CheckControlUI',CheckControlUI)
util.hotfix_ex(CS.DeploymentController,'EndTurnPlayAllData',EndTurnPlayAllData)
util.hotfix_ex(CS.DeploymentController,'GoToBattleScene',GoToBattleScene)
util.hotfix_ex(CS.DeploymentController,'RequestStartThirdAllyTeamTurnHandle',RequestStartThirdAllyTeamTurnHandle)
util.hotfix_ex(CS.DeploymentController,'RequestStartEnemyTurnHandle',RequestStartEnemyTurnHandle)
util.hotfix_ex(CS.DeploymentController,'CheckUIOneLayer',CheckUIOneLayer)



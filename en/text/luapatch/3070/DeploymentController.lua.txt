local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentFriendlyTeamController)
xlua.private_accessible(CS.DeploymentAllyTeamController)
xlua.private_accessible(CS.DeploymentEnemyTeamController)
xlua.private_accessible(CS.DeploymentSquadTeamController)
xlua.private_accessible(CS.DeploymentVehicleTeamController)
xlua.private_accessible(CS.DeploymentBuildingController)
local FindBuffActionFriendly = function(self)
	if CS.GameData.missionAction == nil then
		return;
	end
	local keys = {}
	for key in pairs(CS.GameData.missionAction.listFriendBuffAction) do
		table.insert(keys, key)
	end
	for v,key in ipairs(keys) do
		local value = CS.GameData.missionAction.listFriendBuffAction[key];
		if value.deploymentTeam == self.listGunInTeam then
			value:RefreshUI();
		end
	end
end

local FindBuffActionAlly = function(self)
	if CS.GameData.missionAction == nil then
		return;
	end
	local keys = {}
	for key in pairs(CS.GameData.missionAction.listAllyBuffAction) do
		table.insert(keys, key)
	end
	for v,key in ipairs(keys) do
		local value = CS.GameData.missionAction.listAllyBuffAction[key];
		if value.deploymentTeam == self.allyTeam then
			value:RefreshUI();
		end
	end
end

local FindBuffActionEnemy = function(self)
	if CS.GameData.missionAction == nil then
		return;
	end
	local keys = {}
	for key in pairs(CS.GameData.missionAction.listEnemyBuffAction) do
		table.insert(keys, key)
	end
	for v,key in ipairs(keys) do
		local value = CS.GameData.missionAction.listEnemyBuffAction[key];
		if value.deploymentTeam == self.enemyTeam then
			value:RefreshUI();
		end
	end
end

local FindBuffActionSquad = function(self)
	if CS.GameData.missionAction == nil then
		return;
	end
	local keys = {}
	for key in pairs(CS.GameData.missionAction.listSquadBuffAction) do
		table.insert(keys, key)
	end
	for v,key in ipairs(keys) do
		local value = CS.GameData.missionAction.listSquadBuffAction[key];
		if value.deploymentTeam == self.squadTeam then
			value:RefreshUI();
		end
	end
end

local FindBuffActionVehicle = function(self)
	if CS.GameData.missionAction == nil then
		return;
	end
	local keys = {}
	for key in pairs(CS.GameData.missionAction.listVehicleBuffAction) do
		table.insert(keys, key)
	end
	for v,key in ipairs(keys) do
		local value = CS.GameData.missionAction.listVehicleBuffAction[key];
		if value.deploymentTeam == self.vehicleTeam then
			value:RefreshUI();
		end
	end
end
local Show = function(self,team)
	self:Show(team);
	self.transform:SetAsLastSibling();
end

local InitCode = function(self,code)
	self:InitCode(code);
	if self.spineHolder ~= nil then
		local pos = self.spineHolder.transform.localPosition;
		self.spineHolder.transform.localPosition = CS.UnityEngine.Vector3(pos.x,pos.y,80);
	end
end
local OnClickButton = function(self,Button)
	if CS.CommonConfirmBoxControllerNew.hasOpen then
		return;
	end
	self:OnClickButton(Button);
end
util.hotfix_ex(CS.DeploymentFriendlyTeamController,'FindBuffAction',FindBuffActionFriendly)
util.hotfix_ex(CS.DeploymentAllyTeamController,'FindBuffAction',FindBuffActionAlly)
util.hotfix_ex(CS.DeploymentEnemyTeamController,'FindBuffAction',FindBuffActionEnemy)
util.hotfix_ex(CS.DeploymentSquadTeamController,'FindBuffAction',FindBuffActionSquad)
util.hotfix_ex(CS.DeploymentVehicleTeamController,'FindBuffAction',FindBuffActionVehicle)
util.hotfix_ex(CS.DeploymentVehicleInfoController,'Show',Show)
util.hotfix_ex(CS.DeploymentBuildingController,'InitCode',InitCode)
util.hotfix_ex(CS.DeploymentUIController,'OnClickButton',OnClickButton)
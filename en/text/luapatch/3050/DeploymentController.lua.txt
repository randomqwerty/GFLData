local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentController)
xlua.private_accessible(CS.DeploymentSquadInfoController)
xlua.private_accessible(CS.DeploymentEnemyInfoNew)
local ReastSkillCD = function(self)
	self:ReastSkillCD();
	if self.currentSelectedTeam.vehicleTeam ~= nil then
		self.currentSelectedTeam.vehicleTeam.skill1cdTurn = 0;
		self.currentSelectedTeam.vehicleTeam.skill2cdTurn = 0;
		self.currentSelectedTeam.vehicleTeam.skill3cdTurn = 0;
	end
end

local Show = function(self,squadTeamController)
	self.gameObject:SetActive(true);
	self:Show(squadTeamController);
end
local ShowAllySquad = function(self,allyTeamController)
	if allyTeamController.allyTeam.friendSquadTeam.squadData.info.type>3 then
		self.gameObject:SetActive(false);
		return;
	end
	self.gameObject:SetActive(true);
	self:ShowAllySquad(allyTeamController);
end
local RefreshUI = function(self)
	if self.teamController == nil then
		return;
	end
	if not self.gameObject.activeInHierarchy then
		return;
	end
	self:RefreshUI();
end
local ShowSquadTeam = function(self,squadTeam)
	local type = squadTeam.squadData.info.type;
	if type >3 then
		squadTeam.squadData.info.type = 3;
	end
	self:ShowSquadTeam(squadTeam);
	squadTeam.squadData.info.type = type;
end
local ShowMapInfo = function(self)
	self:ShowMapInfo();
	self.squadTrans.gameObject:SetActive(false);
	self.vehicleTrans.gameObject:SetActive(false);
end
util.hotfix_ex(CS.DeploymentController,'ReastSkillCD',ReastSkillCD)
util.hotfix_ex(CS.DeploymentSquadInfoController,'Show',Show)
util.hotfix_ex(CS.DeploymentSquadInfoController,'ShowAllySquad',ShowAllySquad)
util.hotfix_ex(CS.DeploymentSquadInfoController,'RefreshUI',RefreshUI)
util.hotfix_ex(CS.DeploymentEnemyInfoNew,'ShowSquadTeam',ShowSquadTeam)
util.hotfix_ex(CS.DeploymentEnemyInfoNew,'ShowMapInfo',ShowMapInfo)
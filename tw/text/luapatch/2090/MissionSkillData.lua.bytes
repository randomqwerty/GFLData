local util = require 'xlua.util'

local CheckTeam = function(self)
	self:CheckTeam();
	if self.Team == nil or self.Team:isNull() then
		if self.enemyInstanceId ~= 0 then
			for i=0,CS.DeploymentBackgroundController.Instance.listSpot.Count-1 do
				local spot = CS.DeploymentBackgroundController.Instance.listSpot[i];
				if spot.spotAction.enemyInstanceId == self.enemyInstanceId then
					local play = spot.layer == CS.DeploymentBackgroundController.currentlayer;
					print("hurt创建Enemy"..self.enemyInstanceId);
					local enemy = CS.GameData.missionAction.listEnemyTeams:GetDataById(self.enemyInstanceId);
					enemy.hpPercent = 1;
					CS.DeploymentController.Instance:CreateTeam(spot, 0, CS.DeploymentController.TeamType.enemyTeam, play);
				end
			end
				
		end
		if self.allyInstanceId ~= 0 then
			for i=0,CS.DeploymentBackgroundController.Instance.listSpot.Count-1 do
				local spot = CS.DeploymentBackgroundController.Instance.listSpot[i];
				if spot.spotAction.allyTeamInstanceIds:Contains(self.allyInstanceId) then
					local play = spot.layer == CS.DeploymentBackgroundController.currentlayer;
					print("hurt创建Enemy"..self.allyInstanceId);
					local ally = CS.GameData.missionAction.listAllyTeams:GetDataById(self.allyInstanceId);
					ally.hpPercent = 1;
					CS.DeploymentController.Instance:CreateTeam(spot, 0, CS.DeploymentController.TeamType.allyTeam, play);	
				end
			end
		end
	end
end

util.hotfix_ex(CS.HurtAction,'CheckTeam',CheckTeam)
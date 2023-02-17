local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentEnemyFloatingSpotInfo)

local Awake = function(self)
	self:Awake();
	self.power = 0;
end

local Init = function(self,teamId,deploymentTeamController)
	self:Init(teamId,deploymentTeamController);
	self:RefreshBuffUI();
end
util.hotfix_ex(CS.DeploymentEnemyFloatingSpotInfo,'Awake',Awake)
util.hotfix_ex(CS.DeploymentEnemyFloatingSpotInfo,'Init',Init)



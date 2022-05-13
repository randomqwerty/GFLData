local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentAllyTeamController)


local allyTeamController = nil;
function CheckScale()
	allyTeamController.ScaleX = 100;
end
local RefreshTeam = function(self)
	self:RefreshTeam();
	allyTeamController = self;
	CS.DeploymentController.AddAction(CheckScale,0.4);
end

util.hotfix_ex(CS.DeploymentAllyTeamController,'RefreshTeam',RefreshTeam)




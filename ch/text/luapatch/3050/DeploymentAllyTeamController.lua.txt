local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentAllyTeamController)

local Complete = function(self)
	if CS.DeploymentController.Instance.currentSelectedTeam == nil and CS.DeploymentController.Instance.exchanedSelectedTeam == nil then
		CS.DeploymentController.Instance.currentSelectedTeam = self;
	end
	self:Complete();
end

local PlayMoveShound = function(self)
	self:MoveAction();
	self:PlayMoveShound();
end
util.hotfix_ex(CS.DeploymentAllyTeamController,'Complete',Complete)
util.hotfix_ex(CS.DeploymentAllyTeamController,'PlayMoveShound',PlayMoveShound)
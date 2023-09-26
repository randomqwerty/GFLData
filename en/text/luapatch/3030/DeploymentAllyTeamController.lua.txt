local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentAllyTeamController)

local Complete = function(self)
	self:Complete();
	if self.allyTeam.currentBelong == CS.TeamBelong.friendly then
		if self.allyTeam.vehicleTeam ~= nil then
			CS.CommonAudioController.PlayUI("Stop_UI_loop");
		end
	end
end


util.hotfix_ex(CS.DeploymentAllyTeamController,'Complete',Complete)

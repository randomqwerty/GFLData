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

local CanFreeApMove = function(self)
	if self:isVehicleTeam() then
		return true;
	end
	for i=0,self.currentListBuffAction.Count-1 do
		if self.currentListBuffAction[i].freeApMove then
			return true;
		end
	end
	return false;
end

util.hotfix_ex(CS.DeploymentAllyTeamController,'Complete',Complete)
util.hotfix_ex(CS.DeploymentAllyTeamController,'CanFreeApMove',CanFreeApMove)
local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamInfoController)

local ReinforceSquadTeam = function(self,squadDataController)
	if squadDataController.squad.status ~= CS.SquadStatus.normal then
		CS.CommonController.LightMessageTips(CS.Data.GetLang(1413));
		return;
	end
	self:ReinforceSquadTeam(squadDataController);
end
util.hotfix_ex(CS.DeploymentTeamInfoController,'ReinforceSquadTeam',ReinforceSquadTeam)

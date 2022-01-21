local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamInfoController)

local OnClickTeam = function(self,spot)
	for i=0,self.labelControllers.Length-1 do
		local label = self.labelControllers[i];
		label.gun = nil;
		label.teamid = 0;
		label:Init(i);
	end
	self:OnClickTeam(spot);
end

util.hotfix_ex(CS.DeploymentTeamInfoController,'OnClickTeam',OnClickTeam)




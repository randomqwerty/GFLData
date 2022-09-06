local util = require 'xlua.util'
xlua.private_accessible(CS.AllyTeam)

local CheckTeamType = function(self,jsonData)
	self:CheckTeamType(jsonData);
	if self.allyTeamInfo.allySangvisGunIds.Count > 0 then
		self.useSangvisTeam = true;
	end
end

util.hotfix_ex(CS.AllyTeam,'CheckTeamType',CheckTeamType)




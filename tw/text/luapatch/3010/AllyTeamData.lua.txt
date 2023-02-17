local util = require 'xlua.util'
xlua.private_accessible(CS.AllyTeam)

local CheckTeamType = function(self,jsonData)
	self:CheckTeamType(jsonData);
	if self.allyTeamInfo.allySangvisGunIds.Count > 0 then
		self.useSangvisTeam = true;
	end
end

local currentFairy = function(self)
	local fairy = self.currentFairy;
	if fairy ~= nil then
		if self.showAmmoMre then
			fairy.isFriendFairy = false;
		else
			fairy.isFriendFairy = true;
		end
	end
	return fairy;
end

util.hotfix_ex(CS.AllyTeam,'CheckTeamType',CheckTeamType)
util.hotfix_ex(CS.AllyTeam,'get_currentFairy',currentFairy)




local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentFriendlyTeamController)

local HasGunAlive = function(self)
	if self.teamId > 0 then
		local team = CS.GameData.dictTeam[self.teamId];
		for i=0,team.listGun.Count-1 do
			local gun = team.listGun[i];
			if gun~= nil and gun.life>0 then
				return true;
			end
		end
	elseif self.teamId < 0 then
		local friend = CS.GameData.listFriend:GetDataById(-self.teamId);
		for i=0,friend.useGuns.listGun.listGun.Count-1 do
			local gun = friend.useGuns.listGun[i];
			if gun~= nil and gun.life>0 then
				return true;
			end
		end
	else
		if self.currentSpot.spotAction ~= nil then
			return self.currentSpot.spotAction.hostageHp > 0;
		end
	end
	return false;
end

util.hotfix_ex(CS.DeploymentFriendlyTeamController,'HasGunAlive',HasGunAlive)

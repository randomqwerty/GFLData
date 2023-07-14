local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentSangvisTeamController)

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
		if friend.sangvisTeam ~= nil then
			for i=0,friend.sangvisTeam.listGun.Count-1 do
				local gun = friend.sangvisTeam.listGun[i];
				if gun~= nil and gun.life>0 then
					return true;
				end
			end
		end
	end
	return false;
end

util.hotfix_ex(CS.DeploymentSangvisTeamController,'HasGunAlive',HasGunAlive)

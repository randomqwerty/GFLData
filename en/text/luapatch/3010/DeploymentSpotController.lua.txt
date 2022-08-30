local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentSpotController)

local TeamHasHandgun = function(self)
	if self.currentTeam ~= nil then
		if self.currentTeam.listGunInTeam ~= nil then
			for i=0,self.currentTeam.listGunInTeam.Count-1 do
				local gun = self.currentTeam.listGunInTeam[i];
				if gun ~= nil and gun.info.type == CS.GunType.handgun then
					return true;
				end
			end
		end
		if self.currentTeam.allyTeam ~= nil and self.currentTeam.isFriend then
			for i=0,self.currentTeam.allyTeam.FriendAllyGuns.Count-1 do
				local gun = self.currentTeam.allyTeam.FriendAllyGuns[i];
				if gun.info.type == CS.GunType.handgun then
					return true;
				end
			end
		end
	end
	if self.currentTeamTemp ~= nil then
		if self.currentTeamTemp.listGunInTeam ~= nil then
			for i=0,self.currentTeamTemp.listGunInTeam.Count-1 do
				local gun = self.currentTeamTemp.listGunInTeam[i];
				if gun ~= nil and gun.info.type == CS.GunType.handgun then
					return true;
				end
			end
		end	
		if self.currentTeamTemp.allyTeam ~= nil and self.currentTeamTemp.isFriend then
			for i=0,self.currentTeamTemp.allyTeam.FriendAllyGuns.Count-1 do
				local gun = self.currentTeamTemp.allyTeam.FriendAllyGuns[i];
				if gun.info.type == CS.GunType.handgun then
					return true;
				end
			end
		end
	end
	return false;
end

util.hotfix_ex(CS.DeploymentSpotController,'TeamHasHandgun',TeamHasHandgun)

local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentSpotController)
xlua.private_accessible(CS.DeploymentController)
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

local CheckOther = function(self)
	self:CheckOther();
	for i=0,self.winTypeids.Count-1 do
		self:CloseWinTarget(self.winTypeids[i]);
	end
	self.winTypeids:Clear();
	self.image.raycastTarget = true;
end

local OnFinishAnimationEvent = function(self)
	if CS.GameData.missionAction ~= nil then
		if CS.GameData.missionAction.queueSpotSurroundCapture.Count > 0 then
			CS.DeploymentController.Instance:PlaySpotSurroundCapture();
			return;
		end
	end
	self:OnFinishAnimationEvent();
end
util.hotfix_ex(CS.DeploymentSpotController,'TeamHasHandgun',TeamHasHandgun)
util.hotfix_ex(CS.DeploymentSpotController,'CheckOther',CheckOther)
util.hotfix_ex(CS.DeploymentSpotController,'OnFinishAnimationEvent',OnFinishAnimationEvent)

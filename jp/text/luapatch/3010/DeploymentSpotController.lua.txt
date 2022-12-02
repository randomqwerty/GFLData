local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentSpotController)
xlua.private_accessible(CS.DeploymentController)
xlua.private_accessible(CS.ParticleScaler)
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

local currentlistRoute = function(self)
	self.route:Clear();
	for i=0,self.listRoute.Count-1 do
		local rou = self.listRoute[i];
		if rou ~= nil then
			if not rou.BelongIgnore or not rou.packageIgnore then
				self.route:Add(rou);
			end
		end
	end
	return self.route;
end

local ShowCommonEffect = function(self)
	if self.effect ~= nil and not self.effect:isNull() then
		CS.UnityEngine.Object.DestroyImmediate(self.effect);
	end
	self:ShowCommonEffect();
	if self.effect ~= nil and not self.effect:isNull() then
		local particleScale = self.effect:GetComponent(typeof(CS.ParticleScaler));
		particleScale.start = CS.UnityEngine.Vector2(self.transform.localPosition.x,self.transform.localPosition.y);
	end
end

local Init = function(self)
	self:Init();
	self:ShowCommonEffect();
end
util.hotfix_ex(CS.DeploymentSpotController,'TeamHasHandgun',TeamHasHandgun)
util.hotfix_ex(CS.DeploymentSpotController,'CheckOther',CheckOther)
util.hotfix_ex(CS.DeploymentSpotController,'OnFinishAnimationEvent',OnFinishAnimationEvent)
util.hotfix_ex(CS.DeploymentSpotController,'get_currentlistRoute',currentlistRoute)
util.hotfix_ex(CS.DeploymentSpotController,'ShowCommonEffect',ShowCommonEffect)
util.hotfix_ex(CS.DeploymentSpotController,'Init',Init)

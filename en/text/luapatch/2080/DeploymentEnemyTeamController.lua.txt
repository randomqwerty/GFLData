local util = require 'xlua.util'
local guideDeployment = require("2080/GuideDeploymentController")
xlua.private_accessible(CS.DeploymentEnemyTeamController)

local CheckCurrentSpotTrans = function(self,target)
	if target.currentTeam ~= nil and target.currentTeam:CurrentTeamBelong() == self:CurrentTeamBelong() then
		--target.currentTeam:Die();
		target.currentTeam = nil;
	end
	self:CheckCurrentSpotTrans(target);
end

local CheckFriendTip = function(self)
	if CS.GameData.missionAction == nil then
		return;
	end
	self:CheckFriendTip();
end

local OnPointerUp = function(self,eventData)
	if not canClick then
		return;
	end
	self:OnPointerUp(eventData);
end
util.hotfix_ex(CS.DeploymentEnemyTeamController,'CheckCurrentSpotTrans',CheckCurrentSpotTrans)
util.hotfix_ex(CS.DeploymentEnemyTeamController,'CheckFriendTip',CheckFriendTip)
util.hotfix_ex(CS.DeploymentEnemyTeamController,'OnPointerUp',OnPointerUp)

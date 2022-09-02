local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamController)

local team = nil;

local CheckTeam = function()
	if team.currentSpot.currentTeam == team then
		if team.currentSpot.currentTeamTemp ~= nil then
			team.currentSpot.currentTeam = team.currentSpot.currentTeamTemp;
			team.currentSpot.currentTeamTemp = nil;
		else
			team.currentSpot.currentTeam = nil;
		end
	end
	print("清空",team.currentSpot);
end
--修正梯队被替换数据问题--直接修改会造成第三方敌方交战报错
local Fade = function(self)
	self:Fade();
	team = self;
	CS.DeploymentController.AddAction(CheckTeam,0.01);
end


local Hide = function(self)
	self:Hide();
	team = self;
	CS.DeploymentController.AddAction(CheckTeam,0.01);
end
--修正传送后missionskill面板刷新问题
local TransferComplete = function(self)
	self:TransferComplete();
	self:CheckSpineOrder();
	if CS.DeploymentController.Instance.currentSelectedTeam == self then
		CS.DeploymentController.TriggerSelectTeam(self);
	end
end
--修正夜战小人大角度时的显示
local Start = function(self)
	self:Start();
	if CS.DeploymentController.CurrentMissionInfoIsNight then
		self.offset = CS.UnityEngine.Vector3(0,0,80);
	end
end
util.hotfix_ex(CS.DeploymentTeamController,'Fade',Fade)
util.hotfix_ex(CS.DeploymentTeamController,'Hide',Hide)
util.hotfix_ex(CS.DeploymentTeamController,'TransferComplete',TransferComplete)
--util.hotfix_ex(CS.DeploymentTeamController,'Start',Start)
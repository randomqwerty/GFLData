local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamController)

--修正梯队被替换数据问题
local Fade = function(self)
	self:Fade();
	if self.currentSpot.currentTeam == self and self.currentSpot.currentTeamTemp ~= nil then
		self.currentSpot.currentTeam = self.currentSpot.currentTeamTemp;
		self.currentSpot.currentTeamTemp = nil;
	end
end

local Die = function(self)
	self:Die();
	if self.currentSpot.currentTeam == self and self.currentSpot.currentTeamTemp ~= nil then
		self.currentSpot.currentTeam = self.currentSpot.currentTeamTemp;
		self.currentSpot.currentTeamTemp = nil;
	end
end
--修正传送后missionskill面板刷新问题
local TransferComplete = function(self)
	self:TransferComplete();
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
util.hotfix_ex(CS.DeploymentTeamController,'Die',Die)
util.hotfix_ex(CS.DeploymentTeamController,'TransferComplete',TransferComplete)
--util.hotfix_ex(CS.DeploymentTeamController,'Start',Start)
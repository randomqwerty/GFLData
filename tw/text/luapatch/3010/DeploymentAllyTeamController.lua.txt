local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentAllyTeamController)
xlua.private_accessible(CS.MissionControllerInfo)
local CheckSpecialSpotLine = function(self)
	self:CheckSpecialSpotLine();
	CS.DeploymentController.thirdMissionControllerInfo.otherLineColor = CS.UnityEngine.Color(200/255,140/255,0,1);
end
local RefreshTeam = function(self)
	if self.floatingTeamInfo ~= nil then
		self.floatingTeamInfo.buffItemList:Clear();
	end
	self:RefreshTeam();
	if self.floatingTeamInfo ~= nil then
		self:RefeshBuffUI();
	end
end
util.hotfix_ex(CS.DeploymentAllyTeamController,'CheckSpecialSpotLine',CheckSpecialSpotLine)
util.hotfix_ex(CS.DeploymentAllyTeamController,'RefreshTeam',RefreshTeam)
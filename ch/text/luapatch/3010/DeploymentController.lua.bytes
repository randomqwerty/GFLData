local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentController)

--修正设施延迟刷新
local RequestStartTurnHandle = function(self,json)
	local builds = {};
	for i=0,CS.DeploymentBackgroundController.Instance.listBuildingController.Count -1 do
		local build = CS.DeploymentBackgroundController.Instance.listBuildingController[i];
		table.insert(builds,build);
	end
	CS.DeploymentBackgroundController.Instance.listBuildingController:Clear();
	self:RequestStartTurnHandle(json);
	for i=1,#builds do
		CS.DeploymentBackgroundController.Instance.listBuildingController:Add(builds[i]);
	end
end
--修正设施延迟刷新
local AddAllCanPlayPerformanceLayer = function(self)
	local builds = {};
	for i=0,CS.DeploymentBackgroundController.Instance.listBuildingController.Count -1 do
		local build = CS.DeploymentBackgroundController.Instance.listBuildingController[i];
		table.insert(builds,build);
	end
	CS.DeploymentBackgroundController.Instance.listBuildingController:Clear();
	self:AddAllCanPlayPerformanceLayer();
	for i=1,#builds do
		CS.DeploymentBackgroundController.Instance.listBuildingController:Add(builds[i]);
	end
end

local InitTeamSpots = function(self)
	CS.DeploymentBackgroundController.Instance.listBuildingController:Clear();
	self:InitTeamSpots();
end

util.hotfix_ex(CS.DeploymentController,'RequestStartTurnHandle',RequestStartTurnHandle)
util.hotfix_ex(CS.DeploymentController,'AddAllCanPlayPerformanceLayer',AddAllCanPlayPerformanceLayer)
--util.hotfix_ex(CS.DeploymentController,'InitTeamSpots',InitTeamSpots)



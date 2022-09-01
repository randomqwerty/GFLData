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

local spotid = 0;

local CheckSpot = function()
	local spot = CS.DeploymentBackgroundController.Instance.listSpot:GetDataById(spotid);
	if spot ~= nil and spot.currentTeam == nil and spot.currentTeamTemp ~= nil then
		spot.currentTeam = spot.currentTeamTemp;
		spot.currentTeamTemp = nil;
	end
end

local PlayShowAllTeamForce = function(self,changeData,play)
	self:PlayShowAllTeamForce(changeData,play);
	spotid = changeData.changeData:GetValue("spot_id").Int;
	CS.DeploymentController.AddAction(CheckSpot,2.2);
end
--修正整体UI层级
local InitUIElements = function(self)
	self:InitUIElements();
	self.holderInfo:GetComponent(typeof(CS.UnityEngine.Canvas)).sortingOrder = 2;
	self.uiInfo:GetComponent(typeof(CS.UnityEngine.Canvas)).sortingOrder = 4;
	self.spotInfo:GetComponent(typeof(CS.UnityEngine.Canvas)).sortingOrder = 1;	
	self.OptionInfo:GetComponent(typeof(CS.UnityEngine.Canvas)).sortingOrder = 3;	
end
util.hotfix_ex(CS.DeploymentController,'InitUIElements',InitUIElements)
util.hotfix_ex(CS.DeploymentController,'RequestStartTurnHandle',RequestStartTurnHandle)
util.hotfix_ex(CS.DeploymentController,'AddAllCanPlayPerformanceLayer',AddAllCanPlayPerformanceLayer)
util.hotfix_ex(CS.DeploymentController,'PlayShowAllTeamForce',PlayShowAllTeamForce)



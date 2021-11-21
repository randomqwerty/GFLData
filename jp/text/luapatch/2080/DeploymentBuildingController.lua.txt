local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBuildingController)
xlua.private_accessible(CS.DeploymentMapDragController)

local buildAction = function(self)
	if CS.GameData.missionAction ~= nil then
		local buildAction = CS.GameData.missionAction.listBuildingAction:GetDataById(self.spot.spotInfo.id);
		if buildAction == nil then
			return nil;
		end
		self.spot.buildingAction = buildAction;
		self.spot.spotAction.buildingAction = buildAction;
		buildAction.buildController = self;
		return  buildAction;
	end
	return self.spot.buildingAction;
end

local Init = function(self)
	if self.buildAction == nil then
		return;
	end
	self:Init();
end

local RefreshController = function(self,playcameramove)
	if self.buildAction == nil then
		return;
	end
	self:RefreshController(playcameramove);
end
util.hotfix_ex(CS.DeploymentBuildingController,'get_buildAction',buildAction)
util.hotfix_ex(CS.DeploymentBuildingController,'Init',Init)
util.hotfix_ex(CS.DeploymentBuildingController,'RefreshController',RefreshController)

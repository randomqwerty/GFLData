local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentMapDragController)

local Init = function(self)
	self:Init();
	if CS.DeploymentController.CurrentMissionInfoIsNight then
		self.cameraAngleMax = -10;
	else
		self.cameraAngleMax = -20;
	end
end

local get_mapSize = function(self)
	if self.isScaling then
		self.checkMapSize = self.MapSzieForceMax;
	else
		self.checkMapSize =CS.Mathf.Lerp(self.checkMapSize,6,CS.UnityEngine.Time.deltaTime);
	end
	local size = CS.UnityEngine.Vector2(800,800)*self.checkMapSize;
	return  CS.DeploymentBackgroundController.currentLayerData.mapSize+size;
end

util.hotfix_ex(CS.DeploymentMapDragController,'Init',Init)
util.hotfix_ex(CS.DeploymentMapDragController,'get_mapSize',get_mapSize)

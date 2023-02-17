local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentMapDragController)

local Init = function(self)
	self:Init();
	if CS.DeploymentController.CurrentMissionInfoIsNight then
		self.cameraAngleMax = -10;
	else
		self.cameraAngleMax = -20;
	end
	CS.DeploymentMapDragController.CurrentCamera.nearClipPlane = 1;
end

local get_mapSize = function(self)
	if self.isScaling then
		self.checkMapSize = self.MapSzieForceMax;
	else
		self.checkMapSize =CS.Mathf.Lerp(self.checkMapSize,6,CS.UnityEngine.Time.deltaTime);
	end
	local size = CS.UnityEngine.Vector2(800,800)*self.checkMapSize;
	if CS.DeploymentBackgroundController.currentLayerData ~= nil then
		return  CS.DeploymentBackgroundController.currentLayerData.mapSize+size;
	else
		return size;
	end
end

local ChangeEffectScale = function(self)
	self:ChangeEffectScale();
	if CS.DeploymentBackgroundController.Instance.snowSystem ~= nil and not CS.DeploymentBackgroundController.Instance.snowSystem:isNull() then
		local scale = CS.DeploymentBackgroundController.Instance.snowSystem.transform.localScale;
		CS.DeploymentBackgroundController.Instance.snowSystem.transform.localScale = CS.UnityEngine.Vector3(scale.x,scale.x,scale.z);
	end
end
util.hotfix_ex(CS.DeploymentMapDragController,'Init',Init)
util.hotfix_ex(CS.DeploymentMapDragController,'get_mapSize',get_mapSize)
util.hotfix_ex(CS.DeploymentMapDragController,'ChangeEffectScale',ChangeEffectScale)

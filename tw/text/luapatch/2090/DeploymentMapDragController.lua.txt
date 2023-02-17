local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentMapDragController)

local mapSize = function(self)
	if self.isScaling then
		self.checkMapSize = self.MapSzieForceMax;
	else
		self.checkMapSize = CS.Mathf.Lerp(self.checkMapSize, 1, CS.UnityEngine.Time.deltaTime);
	end
	return CS.DeploymentBackgroundController.currentLayerData.mapSize *self.checkMapSize*1.5;
end

local ReBackView = function(self,action)
	self.targetPosition=CS.DeploymentMapDragController.playerPos;
	self:ReBackView(action);
end
util.hotfix_ex(CS.DeploymentMapDragController,'get_mapSize',mapSize)
util.hotfix_ex(CS.DeploymentMapDragController,'ReBackView',ReBackView)



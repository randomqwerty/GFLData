local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentMapDragController)

local mapSize = function(self)
	if self.isScaling then
		self.checkMapSize = self.MapSzieForceMax;
	else
		self.checkMapSize = CS.Mathf.Lerp(self.checkMapSize, 1.1, CS.UnityEngine.Time.deltaTime);
	end
	return CS.DeploymentBackgroundController.currentLayerData.mapSize *self.checkMapSize;
end

util.hotfix_ex(CS.DeploymentMapDragController,'get_mapSize',mapSize)




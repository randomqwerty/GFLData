local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentMapDragController)

local Init = function(self)
	self:Init();
	if CS.DeploymentController.CurrentMissionInfoIsNight then
		self.cameraAngleMax = 0;
	else
		self.cameraAngleMax = -20;
	end
end

util.hotfix_ex(CS.DeploymentMapDragController,'Init',Init)

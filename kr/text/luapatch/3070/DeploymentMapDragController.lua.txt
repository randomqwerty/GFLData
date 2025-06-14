local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentMapDragController)

local CheckObjDeployment = function(self,obj)
	local check = self:CheckObjDeployment(obj);
	if not check then
		self.pointerDown = false;
	end
	return check
end

local cannotMove = function()
	if CS.DeploymentMapDragController.cannotmove then
		if CS.DeploymentMapDragController.Instance ~= nil then
			CS.DeploymentMapDragController.Instance.pointerDown = false;
		end
	end
	return CS.DeploymentMapDragController.cannotmove;	
end
util.hotfix_ex(CS.DeploymentMapDragController,'get_cannotMove',cannotMove)
util.hotfix_ex(CS.DeploymentMapDragController,'CheckObjDeployment',CheckObjDeployment)
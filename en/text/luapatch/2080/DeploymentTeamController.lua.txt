local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamController)
xlua.private_accessible(CS.DeploymentMapDragController)

local TransferComplete = function(self)
	self:TransferComplete();
	self:RefreshTeamInfo();
end

--local TransferBefore = function(self)
--	self:TransferBefore();
--	local pos = CS.UnityEngine.Vector2(self.transform.localPosition.x,self.transform.localPosition.y);
--	if CS.DeploymentTeamController.transferSpeed > 1 then
--		CS.DeploymentController.TriggerMoveCameraEvent(pos,true,true,true,CS.DeploymentMapDragController.Instance.currentUseMinScale,nil);
--	end
--end
--util.hotfix_ex(CS.DeploymentTeamController,'TransferBefore',TransferBefore)


util.hotfix_ex(CS.DeploymentTeamController,'TransferComplete',TransferComplete)
--util.hotfix_ex(CS.DeploymentTeamController,'Die',Die)


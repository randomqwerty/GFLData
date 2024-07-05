local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBuildingController)

local CheckCodePercent = function(self,playanim)
	if CS.GameData.missionAction == nil then
		self.lastactiveid = self.buildAction.buildingInfo.initial_state;
	end
	self:CheckCodePercent(playanim);
end

util.hotfix_ex(CS.DeploymentBuildingController,'CheckCodePercent',CheckCodePercent)

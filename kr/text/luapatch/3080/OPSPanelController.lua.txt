local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)
xlua.private_accessible(CS.SpecialMissionInfoController)

local active = true;
local CancelMission = function(self)
	active = self.MissionInfoController.gameObject.activeInHierarchy;
	self:CancelMission();
	active = true;
end
local CheckSelectSpotShow= function(self,selectindex,checknull)
	if not active then
		return;
	end
	self:CheckSelectSpotShow(selectindex,checknull);
end

util.hotfix_ex(CS.OPSPanelController,'CancelMission',CancelMission)
util.hotfix_ex(CS.OPSPanelController,'CheckSelectSpotShow',CheckSelectSpotShow)
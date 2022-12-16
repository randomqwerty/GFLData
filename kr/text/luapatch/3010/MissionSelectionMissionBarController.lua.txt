local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionMissionBarController)

local missionbar;
local CheckMission = function()
	missionbar.mission.missionInfo.missionType = CS.MissionType.NormalActivity;
end

local UpdateData = function(self,mission,currentMissionType,MSC,missioninfo)
	self:UpdateData(mission,currentMissionType,MSC,missioninfo);
	if CS.OPSPanelController.Instance ~= nil then
		if self.mission ~= nil and self.mission.autoMissionAction ~= nil then
			if self.mission.missionInfo.missionType == CS.MissionType.NormalActivity then
				missionbar = self;
				self.mission.missionInfo.missionType = CS.MissionType.Activity;
				CS.CommonController.Invoke(CheckMission,0.4,CS.OPSPanelController.Instance);
			end
		end
	end	
end


util.hotfix_ex(CS.MissionSelectionMissionBarController,'UpdateData',UpdateData)
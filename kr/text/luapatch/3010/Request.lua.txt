local util = require 'xlua.util'
xlua.private_accessible(CS.RequestAbortAutoMission)

local _SuccessJsonHandleData = function(self,json)
	if self.text == "1" then
        local info = self.autoMissionAction.info;
        CS.GameData.SetGunStatusToNormal(self.autoMissionAction.listTeamId);
        CS.GameData.listAutoMissionAction:Remove(self.autoMissionAction);

        local ammo = CS.Data.GetAutoCombatResource(info.ammo, self.autoMissionAction.autoTimes);
        local mre = CS.Data.GetAutoCombatResource(info.mre, self.autoMissionAction.autoTimes);
        local mp = CS.Data.GetAutoCombatResource(info.mp, self.autoMissionAction.autoTimes);
        local part = CS.Data.GetAutoCombatResource(info.part, self.autoMissionAction.autoTimes);

        CS.GameData.userInfo:AddUserResource(mp, ammo, mre, part);
        CS.NotificationController.CancelLocalNotification(CS.NotificationController.NotifiType.autoMission, info.missionId);
    else
        self.autoMissionAction:RequestFinishAutoMissionHandler(json);
	end
end


util.hotfix_ex(CS.RequestAbortAutoMission,'SuccessJsonHandleData',_SuccessJsonHandleData)


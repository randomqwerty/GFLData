local util = require 'xlua.util'
xlua.private_accessible(CS.DailyPrizePreviewCtrl)

local mInitMissionDailyDropView = function(self,missionInfo)
	self.selfBtn:GetComponent(typeof(CS.UnityEngine.Canvas)).renderMode=CS.UnityEngine.RenderMode.ScreenSpaceCamera;
	self:InitMissionDailyDropView(missionInfo);
end
local mOpenInDailyGame = function(trans,gunlist,equiplist,difficulty)
	CS.DailyPrizePreviewCtrl.OpenInDailyGame(nil,gunlist,equiplist,difficulty);
end
local mOpenInDailyGameVehicleMission = function(trans,missionInfo)
	CS.DailyPrizePreviewCtrl.OpenInDailyGameVehicleMission(nil,missionInfo);
end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_US then
	util.hotfix_ex(CS.DailyPrizePreviewCtrl,'InitMissionDailyDropView',mInitMissionDailyDropView)
	if CS.ConfigData.clientVersion == "30401" then
		util.hotfix_ex(CS.DailyPrizePreviewCtrl,'OpenInDailyGame',mOpenInDailyGame)
		util.hotfix_ex(CS.DailyPrizePreviewCtrl,'OpenInDailyGameVehicleMission',mOpenInDailyGameVehicleMission)
	end
elseif CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Japan then
	util.hotfix_ex(CS.DailyPrizePreviewCtrl,'OpenInDailyGame',mOpenInDailyGame)
	util.hotfix_ex(CS.DailyPrizePreviewCtrl,'OpenInDailyGameVehicleMission',mOpenInDailyGameVehicleMission)
end	
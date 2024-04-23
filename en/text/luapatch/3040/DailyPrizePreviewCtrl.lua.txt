local util = require 'xlua.util'
xlua.private_accessible(CS.DailyPrizePreviewCtrl)

local mInitMissionDailyDropView = function(self,missionInfo)
	self.selfBtn:GetComponent(typeof(CS.UnityEngine.Canvas)).renderMode=CS.UnityEngine.RenderMode.ScreenSpaceCamera;
	self:InitMissionDailyDropView(missionInfo);

end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_US or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Japan then
	util.hotfix_ex(CS.DailyPrizePreviewCtrl,'InitMissionDailyDropView',mInitMissionDailyDropView)
end

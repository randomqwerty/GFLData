local util = require 'xlua.util'
xlua.private_accessible(CS.DailyPrizePreviewCtrl)

local mOpenInDailyGame = function(trans,gunlist,equiplist,difficulty)
	CS.DailyPrizePreviewCtrl.OpenInDailyGame(nil,gunlist,equiplist,difficulty);
end
local mOpenInDailyGameVehicleMission = function(trans,missionInfo)
	CS.DailyPrizePreviewCtrl.OpenInDailyGameVehicleMission(nil,missionInfo);
end
util.hotfix_ex(CS.DailyPrizePreviewCtrl,'OpenInDailyGame',mOpenInDailyGame)
util.hotfix_ex(CS.DailyPrizePreviewCtrl,'OpenInDailyGameVehicleMission',mOpenInDailyGameVehicleMission)
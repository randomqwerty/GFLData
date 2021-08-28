local util = require 'xlua.util'

local RequestStartAutoMissionSuccess = function(self, www)
    self:SuccessHandleData(www);
	if www.text ~= "1" then
		CS.GameData.userInfo.ammo = CS.GameData.userInfo.ammo - self.autoMissionInfo.ammo * self.autoTimes;
		CS.GameData.userInfo.mre = CS.GameData.userInfo.mre - self.autoMissionInfo.mre * self.autoTimes;
		CS.GameData.userInfo.mp = CS.GameData.userInfo.mp - self.autoMissionInfo.mp * self.autoTimes;
		CS.GameData.userInfo.part = CS.GameData.userInfo.part - self.autoMissionInfo.part * self.autoTimes;
	end
end
util.hotfix_ex(CS.RequestStartAutoMission,'SuccessHandleData',RequestStartAutoMissionSuccess)
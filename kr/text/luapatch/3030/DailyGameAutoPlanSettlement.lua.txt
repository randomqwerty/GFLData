local util = require 'xlua.util'
xlua.private_accessible(CS.DailyGameAutoPlanSettlement)

local Init = function(self,json)
	for i=0,CS.DailyGameAutoPlanController.startPlanhexs.Count-1 do
		local id = CS.DailyGameAutoPlanController.startPlanhexs[i];
		local hexData = CS.DailyExploreData.GetInstance():GetDailyMapHexDict()[id];
		local missionInfo = hexData:GetMission();
		if missionInfo ~= nil then
			if missionInfo.autoMissionInfo ~= nil then
				local gunpool = missionInfo.autoMissionInfo.gunPool;
			end
		end
	end
	self:Init(json);
end
util.hotfix_ex(CS.DailyGameAutoPlanSettlement,'Init',Init)


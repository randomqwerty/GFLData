local util = require 'xlua.util'
xlua.private_accessible(CS.RequestActivityEventPrize)

local SuccessJsonHandleData = function(self,jsonData)
	self:SuccessJsonHandleData(jsonData);
	local temp = CS.System.Collections.Generic.List(CS.OPSEventPrizeData)();
	for i=0,CS.GameData.eventPrizeData.Count-1 do
		if CS.GameData.eventPrizeData[i].prizeLevelInfo.permanent_type == 1 then
			temp:Add(CS.GameData.eventPrizeData[i]);
		end
	end
	for i=0,temp.Count-1 do
		CS.GameData.eventPrizeData:Remove(temp[i]);
	end
end


util.hotfix_ex(CS.RequestActivityEventPrize,'SuccessJsonHandleData',SuccessJsonHandleData)


local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)

local OpenEventPrize = function(self)
	local id = 0;
	for i=0,CS.GameData.eventPrizeData.Count-1 do
		if CS.GameData.eventPrizeData[i].prizeLevelInfo.type == 2 then
			id = CS.GameData.eventPrizeData[i].prizeLevelInfo.id;
		end
	end
	CS.OPSEventPrizeController.OpenInOPS(id);
end


util.hotfix_ex(CS.OPSPanelController,'OpenEventPrize',OpenEventPrize)


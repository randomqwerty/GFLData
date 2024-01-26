local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionController)
local CreateMissionActivityAsyncSuccess = function(self)
	self:CreateMissionActivityAsyncSuccess();
	local index = 0;
	local tags = CS.System.Collections.Generic.List(CS.System.String)();
	for i=0,CS.GameData.listNormalActivityInfo.Count-1 do
		local config = CS.GameData.listNormalActivityInfo[i];
		if not tags:Contains(config.tag) then
			index = index +1;
			config.tagIndex = index;
			tags:Add(config.tag);
		else
			config.tagIndex = index;
		end
	end
end
util.hotfix_ex(CS.MissionSelectionController,'CreateMissionActivityAsyncSuccess',CreateMissionActivityAsyncSuccess)

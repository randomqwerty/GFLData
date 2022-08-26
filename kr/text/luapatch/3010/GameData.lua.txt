local util = require 'xlua.util'
xlua.private_accessible(CS.GameData)
local myGetItem = function(itemid)
	local num = tonumber(itemid);
	if num == nil then
		if itemid ~= nil then
			return CS.GameData.GetItem(itemid);
		end
		return 0;
	elseif num == 10 then
		return CS.GameData.userInfo.core;
	else
		return CS.GameData.GetItem(num);
	end
end

util.hotfix_ex(CS.GameData,'GetItem',myGetItem)
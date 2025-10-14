local util = require 'xlua.util'
xlua.private_accessible(CS.GF.FlightChess.FlightChessPlayerUser)

local zoneId = function(self)
	local uid = tostring(self.userId);
	local zeroid = string.sub(uid, 1, 2);
	if zeroid == "88" then
		return 888;
	end
	if zeroid == "89" then
		return 889;
	end
	return self.zoneId;
end


util.hotfix_ex(CS.GF.FlightChess.FlightChessPlayerUser,'get_zoneId',zoneId)


local util = require 'xlua.util'
xlua.private_accessible(CS.GF.FlightChess.FlightChessPlayerUser)

 
local _DecodeDetailInfo = function(self,jsonData)
	local frame = -1;
	if jsonData:Contains("frame_id") then
		frame = jsonData:GetValue("frame_id").Int;
		if frame >0 then
		self.friendInfo.headFrameId=frame;
		end
	end
	self:DecodeDetailInfo(jsonData);
	
end
util.hotfix_ex(CS.GF.FlightChess.FlightChessPlayerUser,'DecodeDetailInfo',_DecodeDetailInfo)
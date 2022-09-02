local util = require 'xlua.util'
xlua.private_accessible(CS.Friend)
local _Friend = function(self,...)
	local length = select('#', ...);
	if length == 2 then
		local jsondata = select(1, ...);
		local frameId = jsondata:GetValue("frame_id").String;
		self.headFrameId = tonumber(frameId);
	end
end

util.hotfix_ex(CS.Friend,'.ctor',_Friend)
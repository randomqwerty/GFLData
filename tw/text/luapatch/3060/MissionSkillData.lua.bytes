local util = require 'xlua.util'

local PlayEffect = function(self)
	if self.Team == nil then
		--CS.NDebug.LogError("缺少Team",self.teamType);
		return;
	end
	self:PlayEffect();
end

util.hotfix_ex(CS.BuffAction,'PlayEffect',PlayEffect)

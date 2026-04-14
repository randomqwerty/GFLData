local util = require 'xlua.util'
xlua.private_accessible(CS.BuffAction)

local LastEffect = function(self,delay)
	if self.Team == nil then
		return; 
	end
	if self.Team.spineHolder == nil then
		return;
	end
	self:LastEffect(delay);
end
util.hotfix_ex(CS.BuffAction,'LastEffect',LastEffect)

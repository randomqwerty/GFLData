local util = require 'xlua.util'
xlua.private_accessible(CS.FollowCamera)

local Start = function(self)
	self:Start();
	if not self.useawakePos then
		self.transform.localPosition = CS.UnityEngine.Vector3.zero;
	end
end

util.hotfix_ex(CS.FollowCamera,'Start',Start)



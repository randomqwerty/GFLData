local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBuildingController)

local CompleteSpineAnim = function(self)
	if self.skeletonAnimation == nil then
		if self.playAnimHandle ~= nil then
			self.playAnimHandle();
			self.playAnimHandle = nil;
		end
		return;
	end
	self:CompleteSpineAnim();
end

util.hotfix_ex(CS.DeploymentBuildingController,'CompleteSpineAnim',CompleteSpineAnim)

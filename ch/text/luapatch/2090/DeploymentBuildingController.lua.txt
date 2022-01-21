local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBuildingController)

local CompleteSpineAnim = function(self)
	if self.skeletonAnimation ~= nil and not self.skeletonAnimation:isNull() then
		print("CompleteSpineAnim...");
		self.orderanim = CS.Mathf.Min(self.skeletonAnimation.skeleton.Data.Animations.Count - 1, self.orderanim);
		self.currentSpineAnimName = self.skeletonAnimation.skeleton.Data.Animations[self.orderanim].Name;
		self.skeletonAnimation.state:SetAnimation(0, self.currentSpineAnimName, true);
		self.lastactiveid = self.buildAction.activeOrder;
	end
	CS.DeploymentController.AddAction(function()
		if self.playAnimHandle ~= nil then
			self:playAnimHandle();
			self.playAnimHandle = nil;
		end	
	end,0.1);
end

util.hotfix_ex(CS.DeploymentBuildingController,'CompleteSpineAnim',CompleteSpineAnim)

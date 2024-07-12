local util = require 'xlua.util'

Awake = function()
end

Start = function()
	local animName = self.gameObject.name 
	local skeletonAnimation = target:GetComponent(typeof(CS.SkeletonAnimation))
	if skeletonAnimation ~= nil then
		skeletonAnimation.state:SetAnimation(0, animName, true)
	end
end
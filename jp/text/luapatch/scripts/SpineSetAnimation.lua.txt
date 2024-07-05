local util = require 'xlua.util'
local this = {}

Awake = function()
end

Start = function()
	this.animName = self.gameObject.name 
	this.skeletonAnimation = target:GetComponent(typeof(CS.SkeletonAnimation))
end

Update = function()
	this.skeletonAnimation.state:SetAnimation(0, this.animName, true)
end
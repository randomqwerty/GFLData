local util = require 'xlua.util'
local this = {}

Awake = function()
end

Start = function()
	this.transform = self.transform
	this.startPosition = self.transform.localPosition
	this.skeletonAnimation = target:GetComponent(typeof(CS.SkeletonAnimation))
	local boneName = boneNameObj.name
	this.bone = this.skeletonAnimation.skeleton:FindBone(boneName)
end

Update = function()
	if this.bone ~= nil then
		this.transform.localPosition = this.startPosition + CS.UnityEngine.Vector3(this.bone.worldX, this.bone.worldY, 0)
	end
end
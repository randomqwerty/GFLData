local util = require 'xlua.util'
local this = {}

Awake = function()
	this.meshrender = self.transform:GetComponent(typeof(CS.UnityEngine.MeshRenderer));
	this.skeletonAnimation = self.transform:GetComponent(typeof(CS.SkeletonAnimation));
	this.skeletonAnimation.onlyRefreshMaterialsOnStart = true;
	this.matuse = this.meshrender.materials;
	this.meshrender.sharedMaterials = this.matuse;
end

Start = function()	

end

Update = function()
	
end
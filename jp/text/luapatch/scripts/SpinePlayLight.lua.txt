local util = require 'xlua.util'
local this = {}

Awake = function()
	CS.UnityEngine.RenderSettings.ambientLight = CS.UnityEngine.Color(0.2,0.2,0.2,1);
end

Start = function()	
	local shader = CS.ResManager.GetObjectByPath("Shader/SkeletonLight", ".shader");	
	this.meshrender = self.transform:GetComponent(typeof(CS.UnityEngine.MeshRenderer));
	this.skeletonAnimation = self.transform:GetComponent(typeof(CS.SkeletonAnimation));
	this.skeletonAnimation.onlyRefreshMaterialsOnStart = true;
	this.matuse = this.meshrender.materials;
	this.meshrender.sharedMaterials = this.matuse;
	for i=0,this.matuse.Length-1 do
		this.matuse[i].shader = shader;
	end
	for i=0,this.matuse.Length-1 do
		this.matuse[i]:SetFloat("_AMBIENT",1);
	end
end

Update = function()
	
end
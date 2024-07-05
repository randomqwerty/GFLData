local util = require 'xlua.util'
local this = {}
local time = 2;
local delay = 1;
Awake = function()
end

Start = function()
	local shader = CS.ResManager.GetObjectByPath("Shader/SkeletonCloaking", ".shader");
	local mat = CS.ResManager.GetObjectByPath("Material/SkeletonCloaking", ".mat");
	
	this.meshrender = self.transform:GetComponent(typeof(CS.UnityEngine.MeshRenderer));
	this.skeletonAnimation = self.transform:GetComponent(typeof(CS.SkeletonAnimation));
	this.skeletonAnimation.onlyRefreshMaterialsOnStart = true;
	this.matuse = this.meshrender.materials;
	this.meshrender.sharedMaterials = this.matuse;
	for i=0,this.matuse.Length-1 do
		this.matuse[i].shader = shader;
	end
	for i=0,this.matuse.Length-1 do
		local tex = this.matuse[i].mainTexture;
		this.matuse[i]:CopyPropertiesFromMaterial(mat);
		this.matuse[i].mainTexture = tex;
	end
	for i=0,this.matuse.Length-1 do
		this.matuse[i]:DOFloat(1,"_ShowEffect",time):SetDelay(delay);
		this.matuse[i]:DOFloat(5,"_Cutoff",time):SetDelay(delay);
	end
end

Update = function()
	
end
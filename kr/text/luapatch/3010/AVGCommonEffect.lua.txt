local util = require 'xlua.util'
xlua.private_accessible(CS.AVGCommonEffect)

xlua.private_accessible(CS.AVGController)
local InstantiateEffect = function(self,effectPrefab)
	self:InstantiateEffect(effectPrefab);
	local obj = CS.AVGController.Instance.backgroundController.gobjCommonEffect;
	local systems = obj:GetComponentsInChildren(typeof(CS.UnityEngine.ParticleSystem));
	for i=0,systems.Length-1 do
		local render = systems[i]:GetComponent(typeof(CS.UnityEngine.Renderer));
		render.sortingLayerName = "UI";
	end
	local canvas = obj:GetComponentsInChildren(typeof(CS.UnityEngine.Canvas));
	for i=0,canvas.Length-1 do
		canvas[i].sortingLayerName = "UI";
	end
	local meshRenderers = obj:GetComponentsInChildren(typeof(CS.UnityEngine.MeshRenderer));
	for i=0,meshRenderers.Length-1 do
		meshRenderers[i].sortingLayerName = "UI";
	end
end
local _InvokeSpark = function(self)
	self:InvokeSpark();
	if self.goParticleSpark ~=nil then
		local systems = self.goParticleSpark:GetComponent(typeof(CS.UnityEngine.ParticleSystem));
		if systems ~=nil then
			local render = systems:GetComponent(typeof(CS.UnityEngine.Renderer));
			render.sortingLayerName = "UI";
		end
	end 
end
util.hotfix_ex(CS.AVGCommonEffect,'InstantiateEffect',InstantiateEffect)
util.hotfix_ex(CS.AVGController,'InvokeSpark',_InvokeSpark)
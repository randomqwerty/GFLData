local util = require 'xlua.util'
xlua.private_accessible(CS.ParticleScaler)

local Start = function(self)
	self:Start();
	if self.useInDeployment then
		if self.transform.parent ~= nil and self.transform.parent.name == "ImageTarget" then
			self.alsoScaleGameobject = true;
			self.useInDeployment = false;
			for i=0,self.transform.childCount-1 do
				self.transform:GetChild(i).gameObject:SetActive(true);
			end
			self.particleScale = CS.DeploymentMapDragController.scale * self.setSize * 5;
		end
	end
end

util.hotfix_ex(CS.ParticleScaler,'Start',Start)




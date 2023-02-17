local util = require 'xlua.util'
xlua.private_accessible(CS.GuideDeploymentController)

local FinishCurrentStep = function(self)
	if CS.GuideDeploymentController.currentGuideStep == nil then
		return;
	end
	self:FinishCurrentStep();
end
local SelectSpot = function(self,spotid)
	local spot = CS.DeploymentBackgroundController.Instance.listSpot:GetDataById(spotid);
	if spot ~= nil and spot.CannotSee then
		return false;
	end
	return self:SelectSpot(spotid);
end
local Mask = function(self)
	if self.target~=nil and not self.target:isNull() and self.target.root == CS.ImageBufferBlurRefraction.MessageboxCanvas.transform then
		CS.GuideDeploymentController.camera = CS.ImageBufferBlurRefraction.depthonlyCamain;
	end
	self:Mask();
end
util.hotfix_ex(CS.GuideDeploymentController,'FinishCurrentStep',FinishCurrentStep)
util.hotfix_ex(CS.GuideDeploymentController,'SelectSpot',SelectSpot)
util.hotfix_ex(CS.GuideDeploymentController,'Mask',Mask)


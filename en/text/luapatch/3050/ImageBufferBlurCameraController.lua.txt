local util = require 'xlua.util'
xlua.private_accessible(CS.ImageBufferBlurCameraController)
xlua.private_accessible(CS.ImageBufferBlurRefraction)

local SetCanvas = function(self,blurcanvas)
	if blurcanvas.blurImage ~= nil then
		local blur = blurcanvas.blurImage.transform:GetComponent(typeof(CS.ImageBufferBlurRefraction));
		blurcanvas.blurImage.material = blur.showGrabMat;
	end
	self:SetCanvas(blurcanvas);
end

local RevertCanvas = function(self,blurcanvas)
	self:RevertCanvas(blurcanvas);
	if blurcanvas.blurImage ~= nil then
		blurcanvas.blurImage.enabled = true;
		blurcanvas.blurImage.material = nil;		
	end
end
util.hotfix_ex(CS.ImageBufferBlurCameraController,'SetCanvas',SetCanvas)
util.hotfix_ex(CS.ImageBufferBlurCameraController,'RevertCanvas',RevertCanvas)


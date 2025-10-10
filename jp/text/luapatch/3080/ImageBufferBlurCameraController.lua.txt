local util = require 'xlua.util'
xlua.private_accessible(CS.ImageBufferBlurCameraController)
xlua.private_accessible(CS.ImageBufferBlurRefraction)
local CopyConfig = function(self)
	self:CopyConfig();
	if self.camerarecored ~= nil and not self.camerarecored:isNull() then
		CS.ImageBufferBlurRefraction._depthonlyCamera.fieldOfView = self.camerarecored.fieldOfView;
	end
end
local Start = function(self)
	self:Start();
	local pos = self.transform.localPosition;
	self.transform.localPosition = CS.UnityEngine.Vector3(pos.x,pos.y,0);
end
util.hotfix_ex(CS.ImageBufferBlurCameraController,'CopyConfig',CopyConfig)
util.hotfix_ex(CS.ImageBufferBlurRefraction,'Start',Start)
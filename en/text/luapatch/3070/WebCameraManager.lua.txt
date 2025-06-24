local util = require 'xlua.util'
xlua.private_accessible(CS.WebCameraManager)

local Update = function(self)
	if self._webCamera == nil then
		return;
	end
	self:Update();
end


local Start = function(self)
	self:Start();
	--if CS.ResCenter.applicationPlatform == CS.UnityEngine.RuntimePlatform.IPhonePlayer then
		util.hotfix_ex(CS.WebCameraManager,'Update',Update)
	--end
end

util.hotfix_ex(CS.WebCameraManager,'Start',Start)



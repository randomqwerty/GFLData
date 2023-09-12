local util = require 'xlua.util'
xlua.private_accessible(CS.Live2DModelController)

local StartMotion_New = function(self, ...)
	local res = self:StartMotion(...)
	local index = string.find(self.live2DPath,"HK433")

	if res ~= -1 and index ~= nil then
		--CS.NDebug.LogError(self.live2DPath)
		self._motionController:SetLayerAdditive(1, false)
	end

end

util.hotfix_ex(CS.Live2DModelController,'StartMotion',StartMotion_New)

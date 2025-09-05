local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisCaptureController)

local mOpenResultBox = function(self)
	CS.CommonAudioController.StopAllSound();
	--print("Stop scanner")
	self:OpenResultBox()
end
util.hotfix_ex(CS.SangvisCaptureController,'OpenResultBox',mOpenResultBox)
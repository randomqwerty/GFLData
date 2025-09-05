local util = require 'xlua.util'
xlua.private_accessible(CS.PlayerRecallCtrl)

local PlayerTopVideo = function(self,loop)
	if self.movieController.player == nil then
		CS.NDebug.Log("movieController.player为空");
		self.movieController:PlayerManualInitialize();
	end
	self:PlayerTopVideo(loop);
end
util.hotfix_ex(CS.PlayerRecallCtrl,'PlayerTopVideo',PlayerTopVideo)
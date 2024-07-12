local util = require 'xlua.util'
xlua.private_accessible(CS.AVGController)

local OnClickDestroy = function(self)
	if CS.CommonVideoPlayer.InstanceExitAndCanUse then
		CS.CommonVideoPlayer.Instance:Close();
	end
	self:OnClickDestroy();
end

util.hotfix_ex(CS.AVGController,'OnClickDestroy',OnClickDestroy)



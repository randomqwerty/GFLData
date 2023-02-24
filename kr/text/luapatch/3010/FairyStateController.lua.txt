local util = require 'xlua.util'
xlua.private_accessible(CS.FairyStateController)
xlua.private_accessible(CS.ShareButtonController)
local myStart = function(self)
	self:Start();
	self.transform:Find("Left/ShareButton"):GetComponent(typeof(CS.ShareButtonController)).enabled = true;
end
util.hotfix_ex(CS.FairyStateController,'Start',myStart)
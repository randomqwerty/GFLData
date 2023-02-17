local util = require 'xlua.util'
xlua.private_accessible(CS.ResDownloadProcess)

local Show = function(self)
	CS.ResDownloadProcess.agreeDownloadNetWork = true;
	self:Show();
end

util.hotfix_ex(CS.ResDownloadProcess,'Show',Show)

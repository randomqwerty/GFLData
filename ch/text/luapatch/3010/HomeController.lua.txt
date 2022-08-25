local util = require 'xlua.util'
xlua.private_accessible(CS.HomeController)
xlua.private_accessible(CS.ResCenter)

local SevenLoginHandler = function(self)
	self:SevenLoginHandler(); 
	if CS.ResCenter.instance.currentDownloadState == CS.ResCenter.DownloadAddState.HasDownload then
		if CS.ResCenter.instance.resDownload ~= nil and not CS.ResCenter.instance.resDownload:isNull() then
			CS.ResCenter.instance.resDownload:Hide();
		end
	end
end

util.hotfix_ex(CS.HomeController,'SevenLoginHandler',SevenLoginHandler)






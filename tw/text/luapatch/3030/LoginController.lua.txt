local util = require 'xlua.util'
xlua.private_accessible(CS.LoginController)
xlua.private_accessible(CS.GF1.LogFile)

local mReportUpload = function(self)
	--self:ReportUpload();
	self:Start()
	if CS.Data.CanUploadCrash() == false and CS.GF1.LogFile.Instance._threadRunning==true then
		CS.GF1.LogFile.Instance:Shutdown();
		print("log shut down");
	end
end
util.hotfix_ex(CS.LoginController,'Start',mReportUpload)
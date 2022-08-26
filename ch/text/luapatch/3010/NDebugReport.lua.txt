local util = require 'xlua.util'
xlua.private_accessible(CS.NDebugReport)
local myProcessExceptionReport = function(condition, stackTrace, type)

	if type == CS.UnityEngine.LogType.Error then
    else
        CS.NDebugReport.ProcessExceptionReport(condition, stackTrace, type)
    end
end
util.hotfix_ex(CS.NDebugReport,'ProcessExceptionReport',myProcessExceptionReport)
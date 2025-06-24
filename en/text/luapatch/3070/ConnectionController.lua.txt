local util = require 'xlua.util'
xlua.private_accessible(CS.ConnectionController)
xlua.private_accessible(CS.Request)
local EnqueueAndRequest = function(request)
	if CS.ConnectionController.currentRequest ~= nil then
		if CS.ConnectionController.currentRequest.sceneName ~= CS.Utility.loadedLevelName then
			if CS.ConnectionController.currentRequest.timeOut then
				CS.ConnectionController.existsRequest = false;
			end
		end
	end
	CS.ConnectionController.EnqueueAndRequest(request);	
end

local ReLogin = function()
	CS.CommonSceneManagerController.instance.needResetBuildScene = false;
	CS.ConnectionController.ReLogin();
end
--local CheckWWWError = function(self,www,silent,message)
--	local type = self:CheckWWWError(www,silent,message);
--	local index = string.find(www.text,"error:300");
--	if index ~= nil then
--		type = CS.ErrorType.retry;
--	end
	--CS.NDebug.Log(www.text);
--	return type,message;
--end

util.hotfix_ex(CS.ConnectionController,'EnqueueAndRequest',EnqueueAndRequest)
util.hotfix_ex(CS.ConnectionController,'ReLogin',ReLogin)
--util.hotfix_ex(CS.Request,'CheckWWWError',CheckWWWError)

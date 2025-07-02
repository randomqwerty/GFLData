local util = require 'xlua.util'
xlua.private_accessible(CS.ConnectionController)

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

util.hotfix_ex(CS.ConnectionController,'EnqueueAndRequest',EnqueueAndRequest)
util.hotfix_ex(CS.ConnectionController,'ReLogin',ReLogin)


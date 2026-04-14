local util = require 'xlua.util'
xlua.private_accessible(CS.HomeEventController)

local mOpenEvent = function(jumpType)
	CS.HomeEventController.canShowEvent=true;
	if CS.CommonController.sceneJumpName=="Home"then 
		CS.HomeEventController.OpenEvent(jumpType)
	elseif CS.CommonController.sceneJumpName=="" and CS.Utility.loadedLevelName=="Home" then
		CS.HomeEventController.OpenEvent(jumpType)
	end 
end
util.hotfix_ex(CS.HomeEventController,'OpenEvent',mOpenEvent)
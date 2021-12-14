local util = require 'xlua.util'
xlua.private_accessible(CS.GFCriServerWrapper)
local myOnApplicationFocus = function(self, flag)
    if CS.ApplicationConfigData.PlatformChannelId == "ios" then
		
    else
		self:OnApplicationFocus(flag)
    end
end
local myOnApplicationPause = function(self, flag)
    if CS.ApplicationConfigData.PlatformChannelId == "ios" then
		
    else
		self:OnApplicationPause(flag)
    end
end
util.hotfix_ex(CS.GFCriServerWrapper,'OnApplicationFocus',myOnApplicationFocus)
util.hotfix_ex(CS.GFCriServerWrapper,'OnApplicationPause',myOnApplicationPause)
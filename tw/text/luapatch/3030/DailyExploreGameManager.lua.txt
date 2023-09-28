local util = require 'xlua.util'
xlua.private_accessible(CS.DailyExploreGameManager)

local DailyExploreGameManager_OnDestroy = function(self)
	
end


util.hotfix_ex(CS.DailyExploreGameManager,'OnDestroy',DailyExploreGameManager_OnDestroy)
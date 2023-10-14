local util = require 'xlua.util'
xlua.private_accessible(CS.DailyExploreGameManager)

local DailyExploreGameManager_OnDestroy = function(self)
	self:StopAllCoroutines();
	if self.gameObject ~=nil then
		CS.Utility.Destroy(self.gameObject);
		--print("destory DailyExploreGameManager_OnDestroy");
	end
	CS.DailyExploreGameManager.Instance=nil;
end


util.hotfix_ex(CS.DailyExploreGameManager,'OnDestroy',DailyExploreGameManager_OnDestroy)
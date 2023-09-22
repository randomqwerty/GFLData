local util = require 'xlua.util'
xlua.private_accessible(CS.HomeController)
xlua.private_accessible(CS.GF.Common.ObjectPool)

local ResClean = function(deep)
	if CS.Utility.loadedLevelName ~= "Deployment" and CS.Utility.loadedLevelName ~= "Cutin" and CS.Utility.loadedLevelName ~= "Battle" then
		CS.DynamicDataCache.Instance.cacheDataMap:Clear();
		CS.SkeletonDataAsset.saveSkeletonDataTemp:Clear();
		local iter = CS.GF.Common.ObjectPool.Instance.sence2Prefab:GetEnumerator();
		while iter:MoveNext() do
			local name = iter.Current.Key;
			CS.GF.Common.ObjectPool.DestroyAll(name);
		end
		print("ClearRes");
	end
	CS.ResManager.ResClean(deep);
end

local Awake = function(self)
	self:Awake()
	util.hotfix_ex(CS.ResManager,'ResClean',ResClean)
end
util.hotfix_ex(CS.HomeController,'Awake',Awake)
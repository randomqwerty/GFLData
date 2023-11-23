local util = require 'xlua.util'
xlua.private_accessible(CS.HomeController)
xlua.private_accessible(CS.GF.Common.ObjectPool)
xlua.private_accessible(CS.ResDownloadProcess)
xlua.private_accessible(CS.SkeletonDataAsset)
xlua.private_accessible(CS.DynamicDataCache)
xlua.private_accessible(CS.ResManager)
xlua.private_accessible(CS.HomeTeamListBarController)
local ResClean = function(deep)
	if CS.Utility.loadedLevelName ~= "Deployment" and CS.Utility.loadedLevelName ~= "Cutin" and CS.Utility.loadedLevelName ~= "Battle" then
		CS.DynamicDataCache.Instance.cacheDataMap:Clear();
		CS.SkeletonDataAsset.saveSkeletonDataTemp:Clear();
		CS.GF.Common.ObjectPool.tempList:Clear();
		CS.GF.Common.ObjectPool.Instance.sence2Prefab:Clear();
		CS.GF.Common.ObjectPool.Instance.pathPrefabs:Clear();
		CS.GF.Common.ObjectPool.Instance.spawnedObjects:Clear();
		CS.GF.Common.ObjectPool.Instance.pooledObjects:Clear();
		CS.UnityEngine.Object.DestroyImmediate(CS.GF.Common.ObjectPool.Instance.gameObject);
		local iter = CS.ResManager.spineInstanceObj:GetEnumerator();
		while iter:MoveNext() do
			local res = iter.Current.Value;
			if res.prefabInstante ~= nil and not res.prefabInstante:isNull() then
				CS.UnityEngine.Object.DestroyImmediate(res.prefabInstante);
			end
			res.originalPrefab = nil;
		end
		CS.ResManager.spineInstanceObj:Clear();
		local iter1 = CS.ResManager.url_instancePrefab:GetEnumerator();
		while iter1:MoveNext() do
			local res = iter1.Current.Value;
			if res.prefabInstante ~= nil and not res.prefabInstante:isNull() then
				CS.UnityEngine.Object.DestroyImmediate(res.prefabInstante);
			end
			res.originalPrefab = nil;
		end
		CS.ResManager.url_instancePrefab:Clear();		
	end
	CS.ResManager.currentSprites:Clear();
	CS.ResManager.path_Obj:Clear();
	CS.ResManager.resourceObj:Clear();
	CS.ResManager.allcomponents:Clear();
	CS.ResManager.path_Sprite:Clear();
	CS.ResManager.path_SpriteAplha:Clear();
	if deep then
		local abres = CS.ResManager.abpath_AB:GetEnumerator();
		while abres:MoveNext() do
			local ab = abres.Current.Value;
			if ab ~= nil and not ab:isNull() then
				ab:Unload(false);
			end
		end
		local streamabres = CS.ResManager.streamingabpath_AB:GetEnumerator();
		while streamabres:MoveNext() do
			local ab = streamabres.Current.Value;
			if ab ~= nil and not ab:isNull() then
				ab:Unload(false);
			end
		end
		CS.ResManager.abpath_AB:Clear();
		CS.ResManager.streamingabpath_AB:Clear();
	end
	--CS.UnityEngine.AssetBundle.UnloadAllAssetBundles(false);
	print("ClearRes");
end

local Awake = function(self)
	self:Awake()
	util.hotfix_ex(CS.ResManager,'ResClean',ResClean)
end

local ShowDownLoadJPVoice = function(self)
	if self.resDownload ~= nil and self.resDownload.show then
		CS.CommonController.MessageBox(CS.Data.GetLang(52108));
		return;
	end
	self:ShowDownLoadJPVoice();
end

local ShowDownLoadAddData = function(self)
	if self.resDownload ~= nil and self.resDownload.show then
		CS.CommonController.MessageBox(CS.Data.GetLang(52108));
		return;
	end
	self:ShowDownLoadAddData();
end

local CheckDownloadInHome = function(self)
	if self.resDownload ~= nil and self.resDownload.show then		
		return;
	end
	self:CheckDownloadInHome();
end

local BeginDownLoadAdd = function(self)
	CS.ResCenter.instance.currentDownloadState = CS.ResCenter.DownloadAddState.DownloadAddInHome;
	self:BeginDownLoadAdd();
end
local BeginDownLoadVoice = function(self)
	CS.ResCenter.instance.currentDownloadVoiceState = CS.ResCenter.DownloadVoiceState.DownloadAddInHome;
	self:BeginDownLoadVoice();
end

local _OnLevelWasLoaded = function(self)
	if CS.ResCenter.instance.currentDownloadState == CS.ResCenter.DownloadAddState.DownloadAddInHome then
		self:Show();
	end
	if CS.ResCenter.instance.currentDownloadVoiceState == CS.ResCenter.DownloadVoiceState.DownloadAddInHome then
		self:Show();
	end
	if CS.ResCenter.instance.currentSceneName == "HotUpdate" or CS.ResCenter.instance.currentSceneName == "Login" then
		CS.ResCenter.instance:CancelDownBackground();
		self:Hide();
	elseif CS.ResCenter.instance.currentSceneName == "Battle" then
		self.transform.parent:GetComponent(typeof(CS.UnityEngine.Canvas)).enabled = false;
	end
end

local ShowCurrentMission = function(self)
	if CS.GameData.missionAction == nil then
		return;
	end
	self:ShowCurrentMission();
end
util.hotfix_ex(CS.HomeController,'Awake',Awake)
util.hotfix_ex(CS.ResCenter,'ShowDownLoadJPVoice',ShowDownLoadJPVoice)
util.hotfix_ex(CS.ResCenter,'ShowDownLoadAddData',ShowDownLoadAddData)
util.hotfix_ex(CS.ResCenter,'CheckDownloadInHome',CheckDownloadInHome)
util.hotfix_ex(CS.ResCenter,'BeginDownLoadAdd',BeginDownLoadAdd)
util.hotfix_ex(CS.ResCenter,'BeginDownLoadVoice',BeginDownLoadVoice)
util.hotfix_ex(CS.ResDownloadProcess,'_OnLevelWasLoaded',_OnLevelWasLoaded)
util.hotfix_ex(CS.HomeTeamListBarController,'ShowCurrentMission',ShowCurrentMission)
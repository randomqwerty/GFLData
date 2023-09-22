local util = require 'xlua.util'
xlua.private_accessible(CS.HomeController)
xlua.private_accessible(CS.GF.Common.ObjectPool)
xlua.private_accessible(CS.ResDownloadProcess)

local ResClean = function(deep)
	if CS.Utility.loadedLevelName ~= "Deployment" and CS.Utility.loadedLevelName ~= "Cutin" and CS.Utility.loadedLevelName ~= "Battle" then
		CS.DynamicDataCache.Instance.cacheDataMap:Clear();
		CS.SkeletonDataAsset.saveSkeletonDataTemp:Clear();
		CS.GF.Common.ObjectPool.tempList:Clear();
		CS.UnityEngine.Object.DestroyImmediate(CS.GF.Common.ObjectPool.Instance.gameObject);
		print("ClearRes");
	end
	CS.ResManager.ResClean(deep);
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
util.hotfix_ex(CS.HomeController,'Awake',Awake)
util.hotfix_ex(CS.ResCenter,'ShowDownLoadJPVoice',ShowDownLoadJPVoice)
util.hotfix_ex(CS.ResCenter,'ShowDownLoadAddData',ShowDownLoadAddData)
util.hotfix_ex(CS.ResCenter,'CheckDownloadInHome',CheckDownloadInHome)
util.hotfix_ex(CS.ResCenter,'BeginDownLoadAdd',BeginDownLoadAdd)
util.hotfix_ex(CS.ResCenter,'BeginDownLoadVoice',BeginDownLoadVoice)
util.hotfix_ex(CS.ResDownloadProcess,'_OnLevelWasLoaded',_OnLevelWasLoaded)
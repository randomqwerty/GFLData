local util = require 'xlua.util'
xlua.private_accessible(CS.HomeController)
--xlua.private_accessible(CS.LoginController)
--xlua.private_accessible(CS.Data)
--xlua.private_accessible(CS.HomeAnnouncementEventType)
--print("lua加载成功了")
local myCheckRepeatingFixAndOperation = function(self)
    self:CheckRepeatingFixAndOperation();
	print("debugLuaTest")
	local goodStr = CS.UnityEngine.PlayerPrefs.GetString('AddAppstoreEvent')
	print(CS.UnityEngine.PlayerPrefs.GetString('AddAppstoreEvent'));	
	if(CS.System.String.IsNullOrEmpty(goodStr) == false) then	    
		self:AddiOSEvent();		
	end
end
--local myReportUpload = function()
	--print(CS.UnityEngine.PlayerPrefs.GetString('AddAppstoreEvent'));
	--CS.LoginController.ReportUpload();
	--print("myReportUpload")
	--print(CS.UnityEngine.PlayerPrefs.GetString('AddAppstoreEvent'));
--end
--local myOnApplicationFocus = function(self, isFocus)
	--print("premyOnApplicationFocus");
	--print(CS.UnityEngine.PlayerPrefs.GetString('AddAppstoreEvent'));
	--self:OnApplicationFocus(isFocus);
	--if isFocus and self.refreshFinished then
		--if (CS.HomeEventController.IsActive() == false and CS.PlayerReturnEventCtrl.IsActive() == false and false == (CS.PassOrderController.Instance ~= nil and CS.PassOrderController.Instance.gameObject.activeInHierarchy)) then
			--print("myOnApplicationFocus");
			--print(CS.UnityEngine.PlayerPrefs.GetString('AddAppstoreEvent'));
		--else
			--print(CS.UnityEngine.PlayerPrefs.GetString('AddAppstoreEvent'));
			--self:AddiOSEvent();
			--print("no myOnApplicationFocus");
			--print(CS.UnityEngine.PlayerPrefs.GetString('AddAppstoreEvent'));
		--end
	--end
--end
--local myUpdateServerData = function(self)
	--self:UpdateServerData();
	--print("myUpdateServerData");
	--print(CS.UnityEngine.PlayerPrefs.GetString('AddAppstoreEvent'));
--end
--local mySevenLoginHandler = function(self)
	--self:SevenLoginHandler()
	--if(CS.Data.NeedsAttendance()) then
		--print("no SevenLoginHandler");
		--print(CS.UnityEngine.PlayerPrefs.GetString('AddAppstoreEvent'));
	--else
		--print("SevenLoginHandler");
		--print(CS.UnityEngine.PlayerPrefs.GetString('AddAppstoreEvent'));
	--end
--end
--local myLoadNextAnnouncement = function(self)
	--print("myLoadNextAnnouncement-------------")
	--if(self.queueEventWindows.Count > 0) then
		--local info = self.queueEventWindows:Dequeue();
		--if(info~= nil and info.type == CS.HomeAnnouncementEventType.IOSAppstoreEvent) then
			--if self.queueEventWindows.Count == 0 then
				--CS.PlayerPrefs.DeleteKey("AddAppstoreEvent");
				--print("删除key了-------------")
			--end
		--else
			--self.queueEventWindows:Enqueue(info);
		--end
	--end
	----self:LoadNextAnnouncement()
--end
--util.hotfix_ex(CS.HomeController,'SevenLoginHandler',mySevenLoginHandler)
--util.hotfix_ex(CS.HomeController,'UpdateServerData',myUpdateServerData)
--util.hotfix_ex(CS.HomeController,'OnApplicationFocus',myOnApplicationFocus)
if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_US and CS.ApplicationConfigData.PlatformChannelId == "ios" then
	util.hotfix_ex(CS.HomeController,'CheckRepeatingFixAndOperation',myCheckRepeatingFixAndOperation)
end
--util.hotfix_ex(CS.LoginController,'ReportUpload',myReportUpload)
--util.hotfix_ex(CS.HomeEventController,'LoadNextAnnouncement',myLoadNextAnnouncement)
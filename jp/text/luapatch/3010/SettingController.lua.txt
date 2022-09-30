local util = require 'xlua.util'
xlua.private_accessible(CS.ResCenter)
xlua.private_accessible(CS.SettingController)
local OnClickDownloadVoice = function(self)
	if CS.ResCenter.instance.currentDownloadVoiceState == CS.ResCenter.DownloadVoiceState.HasDownload then
		CS.ResCenter.instance:DecideDownloadFileBefore();
		CS.ResCenter.instance:CompareOldNewData();
		CS.ResCenter.instance:CaculateDownSize();
		if CS.ResCenter.allFileDownTotalSize > 0 then
			CS.ResCenter.instance.newResData.compressJPVoiceDataSize = CS.ResCenter.allFileDownTotalSize;
			CS.ResCenter.instance.newResData.originalJPVoiceDataSize = CS.ResCenter.allFileDownTotalSize;
			CS.ResCenter.instance.currentDownloadVoiceState = CS.ResCenter.DownloadVoiceState.DontDownload;
		end
	end
	self:OnClickDownloadVoice();
end

util.hotfix_ex(CS.SettingController,'OnClickDownloadVoice',OnClickDownloadVoice)
local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionController)

local mChekcMissionSkipButton = function(self,jsonData)
	self:ChekcMissionSkipButton()
	if CS.ApplicationConfigData.PlatformChannelId == "pc" then
		self.btnMissionSkip:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = CS.CommonController.LoadPngCreateSprite("AtlasClips3070/pic_mission_skip_us");
	end
end


if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_US then
	util.hotfix_ex(CS.MissionSelectionController,'ChekcMissionSkipButton',mChekcMissionSkipButton)
end


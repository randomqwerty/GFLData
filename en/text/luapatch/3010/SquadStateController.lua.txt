local util = require 'xlua.util'
xlua.private_accessible(CS.SquadStateController)

local myStart = function(self)
    self:Start()
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal and CS.ApplicationConfigData.PlatformChannelId == "ios" then
		local obj1 = CS.ResManager.GetObjectByPath("AtlasClips3010/InfoPanelInBG");
		if obj1 ~= nil then
			local imageTrans = self.transform:Find("Right/ItemGrid/StateSquad/State2/BackGround"):GetComponent(typeof(CS.UnityEngine.UI.Image));
			imageTrans.sprite = obj1:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite;
		end	
	end
end
util.hotfix_ex(CS.SquadStateController,'Start',myStart)
local util = require 'xlua.util'
xlua.private_accessible(CS.BattleUIController)

local InitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local topTime = self.transform:Find("UI/Top/Top_Time");
		local obj1 = CS.ResManager.GetObjectByPath("AtlasClips2080/战斗UI_时间");
		if obj1 ~= nil then
			topTime:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = obj1:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite;
		end
		local top = self.transform:Find("UI/Top/Top");
		local obj2 = CS.ResManager.GetObjectByPath("AtlasClips2080/战斗UI_倒计时");
		if obj2 ~= nil then
			top:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = obj2:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite;;
		end
		local DM = self.transform:Find("UI/SafeUIRect/DPSSwitch");
		DM:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = CS.CommonController.LoadPngCreateSprite("AtlasClips2080/DMGrankingBTN");
	end
end

util.hotfix_ex(CS.BattleUIController,'InitUIElements',InitUIElements)


local util = require 'xlua.util'
xlua.private_accessible(CS.ReinforcementController)

local Start = function(self)
	self:Start();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_US then
		local image = self.transform:Find("MainController/Top/FullScreen/SafeArea/增援许可栏"):GetComponent(typeof(CS.ExImage));
		local obj1 = CS.ResManager.GetObjectByPath("AtlasClips3040/Reinforcement");
		if obj1 ~= nil then
			image.sprite = obj1:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite;
		end
	end
end
util.hotfix_ex(CS.ReinforcementController,'Start',Start)


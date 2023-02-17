local util = require 'xlua.util'
xlua.private_accessible(CS.FactoryController)

local InitUIElements = function(self)
    self:InitUIElements()
    --print(CS.HotUpdateController.instance.mUsePlatform)
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local obj1 = CS.ResManager.GetObjectByPath("AtlasClips3010/妖精制造");
		if obj1 ~= nil then
			self.btnFairyBuild:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = obj1:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite;
		end		
	end
end
util.hotfix_ex(CS.FactoryController,'InitUIElements',InitUIElements)
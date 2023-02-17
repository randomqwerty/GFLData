local util = require 'xlua.util'
xlua.private_accessible(CS.WishGunEventBoxController)

local InitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		self.imgBackgroundObj:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = CS.CommonController.LoadPngCreateSprite("AtlasClips2080/bg");
		self.imgBackgroundSpObj:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = CS.CommonController.LoadPngCreateSprite("AtlasClips2080/bg-重型");
	end
end

util.hotfix_ex(CS.WishGunEventBoxController,'InitUIElements',InitUIElements)



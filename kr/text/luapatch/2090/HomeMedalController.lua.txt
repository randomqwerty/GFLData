local util = require 'xlua.util'
xlua.private_accessible(CS.HomeMedalController)
local InitData_New = function(self, ...)
	self.OpenEffect = false
    self:InitData(...)
end

local InitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Japan then
		local bg = self.transform:Find("Image_Bg"):GetComponent(typeof(CS.ExImage));		
		bg.sprite = CS.CommonController.LoadPngCreateSprite("AtlasClips2090/bg");
	end
end
util.hotfix_ex(CS.HomeMedalController,'InitData',InitData_New)
util.hotfix_ex(CS.HomeMedalController,'InitUIElements',InitUIElements)
local util = require 'xlua.util'
xlua.private_accessible(CS.CommonClothItemController)
--修正同步异步读取错误
local InitView = function(self)
	self.trailOnCloth = nil;
	self.selectColor = self.originalUniform.currentColor;
	self.imgTryOnIcon:SetActive(false);
	self.imgClothIcon.sprite = CS.CommonController.LoadPngCreateSprite(self.originalUniform.info.IconPath);
end

util.hotfix_ex(CS.CommonClothItemController,'InitView',InitView)




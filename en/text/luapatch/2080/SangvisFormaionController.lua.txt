local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisFormaionController)

local InitUIElements = function(self)
	self:InitUIElements();
	--if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
	self.transform:Find("Cost/Img_Bg"):GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = CS.CommonController.LoadPngCreateSprite("AtlasClips2080/COST");
	--end
end

util.hotfix_ex(CS.SangvisFormaionController,'InitUIElements',InitUIElements)



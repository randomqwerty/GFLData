local util = require 'xlua.util'
xlua.private_accessible(CS.IllustratedBookController)

local Awake = function(self)
	self:Awake();
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		local image = self.transform:Find("Top/ExternLayout/Collect/Image");
		image.gameObject:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = CS.CommonController.LoadPngCreateSprite("AtlasClips2090/圆");
	end
end

util.hotfix_ex(CS.IllustratedBookController,'Awake',Awake)

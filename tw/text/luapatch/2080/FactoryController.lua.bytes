local util = require 'xlua.util'
xlua.private_accessible(CS.FactoryController)

local Awake = function(self)
	self:Awake();
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_US and CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Japan then
		self.btnRetire:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = CS.CommonController.LoadPngCreateSprite("AtlasClips2080/替代人形拆解");
	end
end

util.hotfix_ex(CS.FactoryController,'Awake',Awake)
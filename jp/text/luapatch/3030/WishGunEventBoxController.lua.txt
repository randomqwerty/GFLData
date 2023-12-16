local util = require 'xlua.util'
xlua.private_accessible(CS.FactoryResourceController)
xlua.private_accessible(CS.WishGunEventBoxController)

 
local mBatchDevelop = function(self)
	if self.eventInfo~=nil then
		if self.eventInfo.develop_type==1 then
			CS.FactoryResourceController.type = CS.DevelopType.Gun;
		else
			CS.FactoryResourceController.type = CS.DevelopType.SpecialGun;
		end
	end
	--print(CS.FactoryResourceController.type)
	self:BatchDevelop();
end
local InitUIElements = function(self)
	self:InitUIElements();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local txtPoint = self.transform:Find("FrameWishGunEvent/EventBundle/DetailsGroup/EventReturnGroup/Tex_Return");
		txtPoint:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(32341);
	end
end
util.hotfix_ex(CS.WishGunEventBoxController,'BatchDevelop',mBatchDevelop)
util.hotfix_ex(CS.WishGunEventBoxController,'InitUIElements',InitUIElements)
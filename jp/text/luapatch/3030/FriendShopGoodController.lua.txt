local util = require 'xlua.util'
xlua.private_accessible(CS.FriendShopGoodController)
local Start = function(self)
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local tex = self.transform:Find("HaveMask/Img_HaveBg/Tex_Have"):GetComponent(typeof(CS.ExText));
		tex.text = CS.Data.GetLang(110012);
	end
	self:Start();
end

util.hotfix_ex(CS.FriendShopGoodController,'Start',Start)
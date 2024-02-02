local util = require 'xlua.util'
xlua.private_accessible(CS.CommonBundleConfirmBoxController)

local OnClickSkinDetail = function(self)        
    self:OnClickSkinDetail();
	if self.SkinDisplayBackground.transform.childCount >0 then
		local pic = self.SkinDisplayBackground.transform:GetChild(0).gameObject:GetComponent(typeof(CS.CommonPicController));
		pic:SwitchDamaged(false);
	end
end

util.hotfix_ex(CS.CommonBundleConfirmBoxController,'OnClickSkinDetail',OnClickSkinDetail)

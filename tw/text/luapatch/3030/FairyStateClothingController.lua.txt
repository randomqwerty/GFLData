local util = require 'xlua.util'
xlua.private_accessible(CS.FairyStateClothingController)

local _InitUIElements = function(self)
        if self.goDefaultClothing~=nil then
        self.goDefaultClothing.transform:SetParent(self.tweenClothNamePosition.transform.parent, false);
        end
end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then 
	util.hotfix_ex(CS.FairyStateClothingController,'InitUIElements',_InitUIElements)
end
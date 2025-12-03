local util = require 'xlua.util'
xlua.private_accessible(CS.CommonBundleIconController)

 

local mInit = function(self, icon, giftInfo, itemPackage)
	self:Init(icon, giftInfo, itemPackage)
	self.L2dSign:SetActive(false)
end
util.hotfix_ex(CS.CommonBundleIconController,'Init',mInit)
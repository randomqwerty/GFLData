local util = require 'xlua.util'
xlua.private_accessible(CS.PresentWindowController)

local Init = function(self,itemInfo,amount)
	self.filterType = -1
	self:Init(itemInfo,amount)
end
local CheckPackageType = function(self)
	self:CheckPackageType()
	if self.filterType == 0 then
		self.txtFilterClassTitle.text = CS.Data.GetLang(1709); --LanguageConfig.ELANS_TYPE_COMMON.类型_709
	end
end
util.hotfix_ex(CS.PresentWindowController,'Init',Init)
util.hotfix_ex(CS.PresentWindowController,'CheckPackageType',CheckPackageType)

---------------------------------------------------------------------
-- GFClient (C) CompanyName, All Rights Reserved
-- Created by: AuthorName
-- Date: 2022-11-04 14:15:36
---------------------------------------------------------------------

-- To edit this template in: Data/Config/Template.lua
-- To disable this template, check off menuitem: Options-Enable Template File

---@class CommonCharacterListLabelControlerNew
local util = require 'xlua.util'
xlua.private_accessible(CS.CommonCharacterListLabelControlerNew)
local UpdateInfo = function(self)
	self:UpdateInfo();
	if self.listType == CS.ListType.theater or self.listType == CS.ListType.theateAlterFormation then
		if self.canSelect == CS.Data.GetLang(100028) or self.canSelect == CS.Data.GetLang(100031)
			or self.canSelect == CS.Data.GetLang(100029) or self.canSelect == CS.Data.GetLang(100030) 
			or self.canSelect == CS.Data.GetLang(31849) then
			self.canSelect = "";
		end
		
	end
end
util.hotfix_ex(CS.CommonCharacterListLabelControlerNew,'UpdateInfo',UpdateInfo)
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
		self.canSelect = "";
	end
end
util.hotfix_ex(CS.CommonCharacterListLabelControlerNew,'UpdateInfo',UpdateInfo)
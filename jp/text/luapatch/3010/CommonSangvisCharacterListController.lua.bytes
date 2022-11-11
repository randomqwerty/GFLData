---------------------------------------------------------------------
-- GFClient (C) CompanyName, All Rights Reserved
-- Created by: AuthorName
-- Date: 2022-11-04 14:24:34
---------------------------------------------------------------------

-- To edit this template in: Data/Config/Template.lua
-- To disable this template, check off menuitem: Options-Enable Template File
-- 战区列表去掉铁血状态检查
---@class CommonSangvisCharacterListLabelControllerNew

local util = require 'xlua.util'
xlua.private_accessible(CS.CommonSangvisCharacterListController)
xlua.private_accessible("CommonSangvisCharacterListController+UISetting")
local GetCanSelect = function(self,gun)
	if CS.CommonSangvisCharacterListController.Instance.currentSetting.listType == CS.CommonSangvisCharacterListController.ListType.TheaterAlterFormation then
		
		--铁血备选未向canSelect赋值，这边直接返回true
		return true;
	else
		return self:GetCanSelect(gun);
	end
	
end
util.hotfix_ex(CS.CommonSangvisCharacterListController.UISetting,'GetCanSelect',GetCanSelect)
local util = require 'xlua.util'
xlua.private_accessible(CS.CommonBundleConfirmBoxController)

local get_ItemList3Columns = function(self)
	return self.uiHolder:GetUIElement("FrameMallBundle/Bundle/BundleDetails/ItemListScroll/ItemList3Columns",typeof(CS.UnityEngine.Transform))
end
local get_ItemList3ColumnsSkin = function(self)
	return self.uiHolder:GetUIElement("FrameMallBundle/BundleWithSkin/BundleDetails/ItemListScroll/ItemList3Columns",typeof(CS.UnityEngine.Transform))
end
util.hotfix_ex(CS.CommonBundleConfirmBoxController,'get_ItemList3Columns',get_ItemList3Columns)
util.hotfix_ex(CS.CommonBundleConfirmBoxController,'get_ItemList3ColumnsSkin',get_ItemList3ColumnsSkin)

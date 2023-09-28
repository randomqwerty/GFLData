local util = require 'xlua.util'
xlua.private_accessible(CS.IllusBookVehicleComponentListController)

local OpenComponentDetail_New = function(self, ...)
    self:OpenComponentDetail(...)
    self.commonListControllerNew.gameObject:SetActive(false);
    self.scrollRect.enabled = false;
    self.isShowDetail = true
end


util.hotfix_ex(CS.IllusBookVehicleComponentListController,'OpenComponentDetail',OpenComponentDetail_New)


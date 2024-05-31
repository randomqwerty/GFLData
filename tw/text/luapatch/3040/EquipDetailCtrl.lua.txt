local util = require 'xlua.util'
xlua.private_accessible(CS.EquipDetailCtrl)

local mCheckSuitTap = function(self)
	self:CheckSuitTap();
	if self.isIllusBookDetail == false then
       self.relevantBanner:SetActive(false);
    end
end

util.hotfix_ex(CS.EquipDetailCtrl,'CheckSuitTap',mCheckSuitTap)

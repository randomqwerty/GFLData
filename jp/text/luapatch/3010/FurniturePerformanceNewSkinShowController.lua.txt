local util = require 'xlua.util'
xlua.private_accessible(CS.FurniturePerformanceNewSkinShowController)

local Start = function(self)
	self:Start();
	self.textPrologue.transform:SetAsLastSibling();
	local title = self.transform:Find("Main/Title");
	title:SetAsLastSibling();
end


util.hotfix_ex(CS.FurniturePerformanceNewSkinShowController,'Start',Start)
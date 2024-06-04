local util = require 'xlua.util'
xlua.private_accessible(CS.SquadListController)

local RefreshSelectionUI = function(self)
	self:RefreshSelectionUI();
	self.selectionFormation.gameObject:SetActive(self.showSelectionFormation);
end

util.hotfix_ex(CS.SquadListController,'RefreshSelectionUI',RefreshSelectionUI)


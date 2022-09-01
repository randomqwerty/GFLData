local util = require 'xlua.util'
xlua.private_accessible(CS.SpecialMissionInfoController)

local RefreshEntranceUI = function(self)
	self:RefreshEntranceUI();
	if CS.OPSPanelController.Instance ~= nil then
		if CS.OPSPanelController.Instance.campaionId == -41 then
			self.btnSelectDiffcluty.gameObject:SetActive(false);
		end
	end
end

util.hotfix_ex(CS.SpecialMissionInfoController,'RefreshEntranceUI',RefreshEntranceUI)


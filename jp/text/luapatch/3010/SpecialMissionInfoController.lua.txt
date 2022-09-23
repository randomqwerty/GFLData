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

local RefresCommonUI = function(self)
	self:RefresCommonUI();
	if self.missionInfo.ShowScore then
		self.BossGroove.gameObject:SetActive(false);
	end
end
util.hotfix_ex(CS.SpecialMissionInfoController,'RefreshEntranceUI',RefreshEntranceUI)
util.hotfix_ex(CS.SpecialMissionInfoController,'RefresCommonUI',RefresCommonUI)

local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelSpot)

local Init = function(self)
	local mission = CS.GameData.listMission:GetDataById(self.missionId);
	if mission==nil then
		self.gameObject:SetActive(false);
	else
		self.gameObject:SetActive(true);
	end
end

util.hotfix_ex(CS.OPSPanelSpot,'Init',Init)



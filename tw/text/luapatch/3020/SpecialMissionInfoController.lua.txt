local util = require 'xlua.util'
xlua.private_accessible(CS.SpecialMissionInfoController)

local ShowNewReward = function(self)
	self:ShowNewReward();
	if CS.OPSPanelController.difficulty == 1 then
		if self.opsMission~=nil then
			if self.missionInfo.id == self.opsMission.missionIds[0] then
				self.showtxtNew:Find("AutoLayoutNode/Ex").gameObject:SetActive(false);
			end
		end
	end
end

util.hotfix_ex(CS.SpecialMissionInfoController,'ShowNewReward',ShowNewReward)
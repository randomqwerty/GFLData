local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamBuffItem)

local Refresh = function(self)
	self:Refresh();
	if self.teamController.currentListBuffAction:Contains(self.buffaction) then
		if not CS.System.String.IsNullOrEmpty(self.buffaction.missionBuffInfo.manulcode) then 
			self.gameObject:SetActive(false);
		end
	end
end

util.hotfix_ex(CS.DeploymentTeamBuffItem,'Refresh',Refresh)

local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamController)

local BuffSpecialSpotAddViewEffect = function(self)
	local effect = 0;
	for i=0,self.currentListBuffAction.Count-1 do
		local nightView = self.currentListBuffAction[i].nightView;
		effect = CS.Mathf.Max(effect,nightView);
	end
	return effect;
end

local CheckTeamBothCanMove = function(self,spot)
	if spot.currentHostage ~= nil then
		return self:CheckTeamCanMove(spot) and spot.currentHostage:CheckTeamCanMove(self.currentSpot);
	end
	return self:CheckTeamBothCanMove(spot);
end
util.hotfix_ex(CS.DeploymentTeamController,'BuffSpecialSpotAddViewEffect',BuffSpecialSpotAddViewEffect)
util.hotfix_ex(CS.DeploymentTeamController,'CheckTeamBothCanMove',CheckTeamBothCanMove)
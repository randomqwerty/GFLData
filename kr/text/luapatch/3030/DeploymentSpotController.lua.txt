local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentSpotController)

local RadarEffect = function(self)
	local effect = self:RadarEffect();
	if self.spotAction ~= nil then
		local view = -1;
		for i=0,self.spotAction.listSpecialAction.Count-1 do
			local nightView = self.spotAction.listSpecialAction[i].nightView;
			view = CS.Mathf.Max(view,nightView);
		end
		effect = CS.Mathf.Max(view,effect);
	end
	return effect;
end

local GetNightCurrentShowSpots = function(self)
	local spots = self:GetNightCurrentShowSpots();
	for i=spots.Count - 1, 0, -1 do
		local spot = spots[i];
		if spot.CannotSee then
			spots:RemoveAt(i);
		end
	end
	return spots;
end
util.hotfix_ex(CS.DeploymentSpotController,'RadarEffect',RadarEffect)
util.hotfix_ex(CS.DeploymentSpotController,'GetNightCurrentShowSpots',GetNightCurrentShowSpots)
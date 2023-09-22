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

util.hotfix_ex(CS.DeploymentSpotController,'RadarEffect',RadarEffect)
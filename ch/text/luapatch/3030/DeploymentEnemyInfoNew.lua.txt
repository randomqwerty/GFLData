local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentEnemyInfoNew)

local CheckMapSpecialSpotInfo = function(self)
	for i=0,self.currentSpot.spotAction.listSpecialAction.Count-1 do
		local specialspot = self.currentSpot.spotAction.listSpecialAction[i];
		self.currentSpot.effectSepcialSpot:Remove(specialspot);
	end
	return self:CheckMapSpecialSpotInfo();
end

util.hotfix_ex(CS.DeploymentEnemyInfoNew,'CheckMapSpecialSpotInfo',CheckMapSpecialSpotInfo)

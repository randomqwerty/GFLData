local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentEnemyInfoNew)

local ShowBuildInfo = function(self,spot)
	for i=0,self.buildSpots.Count-1 do
		if self.buildSpots[i] ~= nil then
			if self.buildSpots[i].spot ~= nil then
				self.buildSpots[i].spot:CloseBuildRangeTip();
			end
		end
	end
	self:ShowBuildInfo(spot);
end
util.hotfix_ex(CS.DeploymentEnemyInfoNew,'ShowBuildInfo',ShowBuildInfo)
local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentEnemyFloatingSpotInfo)

local Awake = function(self)
	self:Awake();
	self.power = 0;
end

util.hotfix_ex(CS.DeploymentEnemyFloatingSpotInfo,'Awake',Awake)




local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentEnemyFloatingSpotInfo)


local Awake = function(self)
	self:Awake();
	self.color = CS.UnityEngine.Color(0,0,0,1);
end

util.hotfix_ex(CS.DeploymentEnemyFloatingSpotInfo,'Awake',Awake)


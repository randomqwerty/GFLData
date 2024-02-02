local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentEnemyTeamController)

local CheckFriendTip = function(self)
	if CS.DeploymentBackgroundController.currentLayerData == nil then
		return;
	end
	self:CheckFriendTip();
end

util.hotfix_ex(CS.DeploymentEnemyTeamController,'CheckFriendTip',CheckFriendTip)


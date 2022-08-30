local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentMovingOptionController)

local Open = function(self)
	self:Open();
	CS.UITweenManager.PlayFadeTweens(self.transform, 0, 1, 0.3);
end

util.hotfix_ex(CS.DeploymentMovingOptionController,'Open',Open)

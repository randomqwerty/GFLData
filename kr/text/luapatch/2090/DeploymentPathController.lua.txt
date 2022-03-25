local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentPathController)

local DrawPath = function(self)
	self.gameObject:SetActive(true);
	self:DrawPath();
end

util.hotfix_ex(CS.DeploymentPathController,'DrawPath',DrawPath)




local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBuildSkillItem)

local RefreshLeftUI = function(self)
	self:RefreshLeftUI();
	if self.skillTipTrans.gameObject.activeInHierarchy then
		self:ShowSkillTipContent();
	end
end

util.hotfix_ex(CS.DeploymentBuildSkillItem,'RefreshLeftUI',RefreshLeftUI)

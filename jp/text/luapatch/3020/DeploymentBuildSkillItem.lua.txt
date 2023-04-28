local util = require 'xlua.util'
xlua.private_accessible(CS.BuildSkillDetail)

local RequestControlBuild = function(self,data)
	CS.DeploymentController.Instance:AddAndPlayPerformance(nil);
	self:RequestControlBuild(data);
end

local RequestBuffControlBuild = function(self,data)
	CS.DeploymentController.Instance:AddAndPlayPerformance(nil);
	self:RequestBuffControlBuild(data);
end

local RefreshUI = function(self)
	self:CheckItemCost();
end

local RefreshLeftUI = function(self)
	self:RefreshLeftUI();
	self.btnSkill.gameObject:SetActive(true);
	self.btnSkillCancelLeft.gameObject:SetActive(false);
end
util.hotfix_ex(CS.BuildSkillDetail,'RequestControlBuild',RequestControlBuild)
util.hotfix_ex(CS.BuildSkillDetail,'RequestBuffControlBuild',RequestBuffControlBuild)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'RefreshUI',RefreshUI)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'RefreshLeftUI',RefreshLeftUI)
local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBuildSkillItem)
xlua.private_accessible(CS.DeploymentFriendlyTeamController)
xlua.private_accessible(CS.DeploymentSangvisTeamController)

local RefreshLeftUI = function(self)
	self:RefreshLeftUI();
	if self.skillTipTrans.gameObject.activeInHierarchy then
		self:ShowSkillTipContent();
	end
	self:RefreshUI();
end

local SelectSkillSpot = function(self,spot)
	if CS.UnityEngine.Input.touchCount >1 then
		return;
	end
	self:SelectSkillSpot(spot);
	self:CloseAllSelectTarget();
	CS.DeploymentController.TriggerSelectTeam(nil);
	CS.DeploymentUIController.Instance:OnSelectTeamSkillUI(nil);
end

local ControlBuild = function(self)
	if CS.UnityEngine.Input.touchCount >1 then
		return;
	end
	self:ControlBuild();
end
util.hotfix_ex(CS.DeploymentBuildSkillItem,'RefreshLeftUI',RefreshLeftUI)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'SelectSkillSpot',SelectSkillSpot)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'ControlBuild',ControlBuild)
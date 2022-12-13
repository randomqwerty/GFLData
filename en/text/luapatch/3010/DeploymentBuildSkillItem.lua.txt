local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBuildSkillItem)
xlua.private_accessible(CS.DeploymentFriendlyTeamController)
xlua.private_accessible(CS.DeploymentSangvisTeamController)
xlua.private_accessible(CS.BuildSkillDetail)
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

local checkTeamTrans = function()
	CS.DeploymentController.Instance:CheckTeamTrans();
end

local checkBuildOnDeath = function()
	CS.DeploymentController.Instance:CheckBuildCastSkillOnDeath();
end

local RequestControlBuild = function(self,data)
	self:RequestControlBuild(data);
	if CS.GameData.missionResult ~= nil then
		return;
	end
	if CS.DeploymentController.Instance:HasTeamCanTrans() then
		CS.DeploymentController.Instance:AddAndPlayPerformance(checkTeamTrans);
		CS.DeploymentController.Instance:AddAndPlayPerformance(checkBuildOnDeath);
	end
end
util.hotfix_ex(CS.DeploymentBuildSkillItem,'RefreshLeftUI',RefreshLeftUI)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'SelectSkillSpot',SelectSkillSpot)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'ControlBuild',ControlBuild)
util.hotfix_ex(CS.BuildSkillDetail,'RequestControlBuild',RequestControlBuild)
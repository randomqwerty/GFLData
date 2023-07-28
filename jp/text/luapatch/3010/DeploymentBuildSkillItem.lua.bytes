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

local CheckItemCost = function(self)
	
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

local RequestBuffControlBuild = function(self,data)
	self:CheckCost();
	self:RequestBuffControlBuild(data);
end

local CheckCost = function(self)
	self:CheckCost();
	if self.skill.itemCose.Keys.Count>0 then
		local items = CS.System.Collections.Generic.List(CS.System.Int32)(self.skill.itemCose.Keys);
		for i=0,items.Count-1 do
			local itemid = items[i];
			local costnum = self.skill.itemCose[itemid];
			local totalnum = CS.GameData.GetItem(itemid);
			local resnum = totalnum - costnum;
			print("消耗"..itemid.."数目"..costnum);
			CS.GameData.SetItem(itemid, resnum);
		end
	end
end
util.hotfix_ex(CS.DeploymentBuildSkillItem,'RefreshLeftUI',RefreshLeftUI)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'SelectSkillSpot',SelectSkillSpot)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'ControlBuild',ControlBuild)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'CheckItemCost',CheckItemCost)
util.hotfix_ex(CS.BuildSkillDetail,'RequestControlBuild',RequestControlBuild)
util.hotfix_ex(CS.BuildSkillDetail,'RequestBuffControlBuild',RequestBuffControlBuild)
util.hotfix_ex(CS.BuildSkillDetail,'CheckCost',CheckCost)
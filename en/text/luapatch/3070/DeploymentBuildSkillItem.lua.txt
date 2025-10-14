local util = require 'xlua.util'
xlua.private_accessible(CS.BuildSkillDetail)
xlua.private_accessible(CS.DeploymentBuildSkillItem)
local checkBattle = function()
	CS.DeploymentController.Instance:CheckBattle();
end
local RequestControlBuild = function(self,data)
	self:RequestControlBuild(data);
	if CS.GameData.missionResult == nil then
		CS.DeploymentController.Instance:AddAndPlayPerformance(checkBattle);
	end
end
local RequestBuffControlBuild = function(self,data)
	self:RequestBuffControlBuild(data);
	if CS.GameData.missionResult == nil then
		CS.DeploymentController.Instance:AddAndPlayPerformance(checkBattle);
	end
end
local CheckCastRougeEnd = function(self)
	for i=0,CS.DeploymentUIController.Instance.leftSkills.Count-1 do
		local skill = CS.DeploymentUIController.Instance.leftSkills[i];
		if skill.skillItem ~= nil then
			skill.skillItem.playanim = false;
			skill.skillItem.selectItems:Clear();
		end
	end
	if self.RougeSummerObj ~= nil and self.RougeSummerObj.activeInHierarchy then
		self.selectItems:Clear();
		self:PlayRougeAnim(false);
		self.playanim = false;
		if self.willclose then
			CS.UnityEngine.Object.Destroy(self.RougeSummerObj);
		else
			self:ShowRougeSummerUI();
		end
	end
end
util.hotfix_ex(CS.BuildSkillDetail,'RequestControlBuild',RequestControlBuild)
util.hotfix_ex(CS.BuildSkillDetail,'RequestBuffControlBuild',RequestBuffControlBuild)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'CheckCastRougeEnd',CheckCastRougeEnd)
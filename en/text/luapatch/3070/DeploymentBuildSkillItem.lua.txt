local util = require 'xlua.util'
xlua.private_accessible(CS.BuildSkillDetail)

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
util.hotfix_ex(CS.BuildSkillDetail,'RequestControlBuild',RequestControlBuild)
util.hotfix_ex(CS.BuildSkillDetail,'RequestBuffControlBuild',RequestBuffControlBuild)
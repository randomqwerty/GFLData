local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBuildingController)

local CheckSkillDetail = function(self,skill)
	local check = self:CheckSkillDetail(skill);
	local checkSpots = CS.System.Collections.Generic.List(CS.SpotAction)(); 
	for i=0,skill.targetSpotAction.Count-1 do
		local spotAction = skill.targetSpotAction[i];
		if CS.GameData.currentSelectedMissionInfo.specialType == CS.MapSpecialType.Night then
			if not spotAction.spot.Show then
				checkSpots:Add(spotAction);
			end
		end
	end
	for i=0,checkSpots.Count-1 do
		skill.targetSpotAction:Remove(skill.targetSpotAction[i]);
	end
	return skill.targetSpotAction.Count > 0;
end

util.hotfix_ex(CS.DeploymentBuildingController,'CheckSkillDetail',CheckSkillDetail)

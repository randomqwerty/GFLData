local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamInfoController)

local CanDeployVehicle = function(vehicle,showTip)
	if not showTip then
		local dr = CS.GameData.currentSelectedMissionInfo.difficultyRecommendDetail;
		if dr.Count > 4 and dr[4] ~= CS.UnityEngine.Vector2.zero then
			if vehicle.developScore <= dr[4].x then
				return false;
			end
		end
	end
	return CS.DeploymentTeamInfoController.CanDeployVehicle(vehicle,showTip);
end

local CanDeploySquad = function(squad)
	local dr = CS.GameData.currentSelectedMissionInfo.difficultyRecommendDetail;
	if dr.Count > 3 and dr[3] ~= CS.UnityEngine.Vector2.zero then
		if squad:GetPoint() <= dr[3].x then
			return false;
		end
	end	
	if squad.vehicleId ~= 0 then
		return false;
	end
	return CS.DeploymentTeamInfoController.CanDeploySquad(squad);
end
local CheckTeamMissionRecommand = function(team,allpoint)
	allpoint = 0;
	for i=0,team.listGun.Count-1 do
		local gun = team.listGun[i];
		if CS.DeploymentController.CurrentMissionInfoIsNight then
			allpoint = allpoint + gun:GetPoint(true, false, true, team,true,nil);
		else
			allpoint = allpoint + gun:GetPoint(true, false, false, team,true,nil);
		end
	end
	local dr = CS.GameData.currentSelectedMissionInfo.difficultyRecommendDetail;
	if team.SangvisTeamCurrentCost ~= nil then
		if dr.Count > 1 and dr[1] ~= CS.UnityEngine.Vector2.zero then
			if allpoint <= dr[1].x then
				return false,allpoint;
			end
		end
	else
		if dr.Count > 0 and dr[0] ~= CS.UnityEngine.Vector2.zero then
			if allpoint <= dr[0].x then
				return false,allpoint;
			end
		end
	end
	return true,allpoint;
end
util.hotfix_ex(CS.DeploymentTeamInfoController,'CanDeployVehicle',CanDeployVehicle)
util.hotfix_ex(CS.DeploymentTeamInfoController,'CanDeploySquad',CanDeploySquad)
util.hotfix_ex(CS.DeploymentTeamInfoController,'CheckTeamMissionRecommand',CheckTeamMissionRecommand)

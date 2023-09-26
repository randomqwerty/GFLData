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
	if CS.GameData.currentSelectedMissionInfo.vehicleLimitTeam == -1 then
		return false;
	end
	if CS.GameData.currentSelectedMissionInfo.vehicleLimitTeam ~= 0 and CS.DeploymentController.Instance.VehicleTeamCount >= CS.GameData.currentSelectedMissionInfo.vehicleLimitTeam then
		return false;
	end
	if CS.GameData.currentSelectedMissionInfo.totalTeamLimit>0 and CS.GameData.currentSelectedMissionInfo.basesquadCanTotalTeam then
		if CS.DeploymentController.Instance.TotalTeamsCount >= CS.GameData.currentSelectedMissionInfo.totalTeamLimit then
			return false;
		end
	end
	if vehicle.fake then
		if showTip then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(33048));
		end
		return false;
	end
	if not vehicle:CheckCrewStateNormal() then
		if showTip then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(290103));
		end
		return false;
	end
	if CS.DeploymentController.Instance.squadVehiclePopCost + vehicle.vehicleInfo.population > CS.DeploymentController.Instance.SquadVehicleCanGetPop then
		if showTip then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(33049));
		end
		return false;
	end
	if vehicle.isDamaged then
		if showTip then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(30553));
		end
		return false;
	end
	if vehicle.status ~= CS.VehicleStatus.normal then
		if showTip then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(33048));
		end
		return false;
	end
	if CS.GameData.missionAction ~= nil then
		for i=0,CS.DeploymentController.Instance.vehicleTeams.Count-1 do
			local team = CS.DeploymentController.Instance.vehicleTeams[i];
			if team.vehicleTeam.vehicle == vehicle then
				if showTip then
					CS.CommonController.LightMessageTips(CS.Data.GetLang(33051));
				end
				return false;
			end
		end
		local ap = CS.DeploymentController.Instance:squadTypeApCost(CS.SquadInfoCategory.carrier);
		if CS.GameData.missionAction.ap<ap then
			if showTip then
				CS.CommonController.LightMessageTips(CS.Data.GetLang(33048));
			end
			return false;
		end
	end
	return true;
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
	if CS.GameData.currentSelectedMissionInfo.onlyCanUseVehice then
		return false;
	end
	if CS.GameData.currentSelectedMissionInfo.squadLimitTeam == -1 then
		return false;
	end
	if CS.GameData.currentSelectedMissionInfo.squadLimitTeam ~= 0 and CS.DeploymentController.Instance.SquadTeamsCount >= CS.GameData.currentSelectedMissionInfo.squadLimitTeam then
		return false;
	end
	if CS.GameData.currentSelectedMissionInfo.totalTeamLimit>0 and CS.GameData.currentSelectedMissionInfo.basesquadCanTotalTeam then
		if CS.DeploymentController.Instance.TotalTeamsCount >= CS.GameData.currentSelectedMissionInfo.totalTeamLimit then
			return false;
		end
	end	
	if CS.DeploymentController.Instance.squadVehiclePopCost + squad.info.popcost > CS.DeploymentController.Instance.SquadVehicleCanGetPop then
		return false;
	end
	if squad.life == 0 then
		return false;
	end
	if squad.status ~= CS.SquadStatus.normal then
		return false;
	end
	if CS.GameData.missionAction ~= nil then
		local ap = CS.DeploymentController.Instance:squadTypeApCost(squad.info.infoType);
		if CS.GameData.missionAction.ap<ap then
			return false;
		end
		for i=0,CS.DeploymentController.Instance.squadTeams.Count-1 do
			local team = CS.DeploymentController.Instance.squadTeams[i];
			if team.squadTeam.squadData == squad then
				return false;
			end
		end
	end
	return true;
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

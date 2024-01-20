local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentAutoBattleController)

local FindSupplySpotMainTeamAround = function()
	local target = nil;
	local length = 100;
	local selfteam = CS.DeploymentAutoBattleController.currentAutoMoveStep.team;
	for i=0,CS.DeploymentAutoBattleController.currentAutoMoveStep.assitTeamStep.Count-1 do
		local assitStep = CS.DeploymentAutoBattleController.currentAutoMoveStep.assitTeamStep[i];
		local spots = assitStep.team.currentSpot:GetSpotInRange(2);
		for j=0,spots.Count-1 do
			local spot = spots[j];
			if not selfteam.currentSpot == spot and not CS.DeploymentAutoBattleController.SpotHasHardEnemy(spot) and not CS.DeploymentAutoMoveStep.targetspots:Contains(spot) then
				local ids = CS.DeploymentAutoBattleController.GenAutoRoute(selfteam.currentSpot.spotInfo.id, spot.spotInfo.id, selfteam.layer);
				if CS.DeploymentAutoBattleController.NeedSupply(selfteam) then
					if CS.DeploymentController.CanSquadSupply(spot) then
						if ids.Count > 0 and ids.Count < length then
							target = spot;
							length = ids.Count;
						end
					end
				elseif spot:HasEnemyTeam() then
					if ids.Count > 0 and ids.Count < length then
						target = spot;
						length = ids.Count;
					end
				end		
			end
		end
	end
	return target;
end

local ShouldAssitTeamStop = function(autoMoveStep)
	if autoMoveStep.team:isVehicleTeam() then
		if not CS.DeploymentAutoBattleController.NeedSupply(autoMoveStep.team) then
			return false;
		end
	end
	return CS.DeploymentAutoBattleController.ShouldAssitTeamStop(autoMoveStep);
end
util.hotfix_ex(CS.DeploymentAutoBattleController,'FindSupplySpotMainTeamAround',FindSupplySpotMainTeamAround)
util.hotfix_ex(CS.DeploymentAutoBattleController,'ShouldAssitTeamStop',ShouldAssitTeamStop)
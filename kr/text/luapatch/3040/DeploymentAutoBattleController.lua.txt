local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentAutoBattleController)
xlua.private_accessible(CS.DeploymentAutoMoveStep)
local FindSupplySpotMainTeamAround = function()
	local target = nil;
	local length = 100;
	local selfteam = CS.DeploymentAutoBattleController.currentAutoMoveStep.team;
	for i=0,CS.DeploymentAutoBattleController.currentAutoMoveStep.assitTeamStep.Count-1 do
		local assitStep = CS.DeploymentAutoBattleController.currentAutoMoveStep.assitTeamStep[i];
		local spots = assitStep.team.currentSpot:GetSpotInRange(3);
		for j=0,spots.Count-1 do
			local spot = spots[j];
			if selfteam.currentSpot == spot then				
			elseif CS.DeploymentAutoBattleController.SpotHasHardEnemy(spot) then				
			elseif CS.DeploymentAutoMoveStep.targetspots:Contains(spot) then				
			else
				local ids = CS.DeploymentAutoBattleController.GenAutoRoute(selfteam.currentSpot.spotInfo.id, spot.spotInfo.id, selfteam.layer);
				--print(spot.spotInfo.id.."/"..tostring(ids.Count));
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

local GetID = function(self)
	if self.vehicleTeamId ~= 0 then
		return self.vehicleTeamId*100;
	end
	return self.teamId;
end
util.hotfix_ex(CS.DeploymentAutoBattleController,'FindSupplySpotMainTeamAround',FindSupplySpotMainTeamAround)
util.hotfix_ex(CS.DeploymentAutoBattleController,'ShouldAssitTeamStop',ShouldAssitTeamStop)
util.hotfix_ex(CS.DeploymentAutoMoveStep,'GetID',GetID)
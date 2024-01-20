local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentAutoBattleController)

local FindSupplySpotMainTeamAround = function()
	local target = nil;
	local selfteam = CS.DeploymentAutoBattleController.currentAutoMoveStep.team;
	for i=0,CS.DeploymentAutoBattleController.currentAutoMoveStep.assitTeamStep.Count-1 do
		local assitStep = CS.DeploymentAutoBattleController.currentAutoMoveStep.assitTeamStep[i];
		local spots = assitStep.team.currentSpot:GetSpotInRange(2);
		for j=0,spots.Count-1 do
			local spot = spots[j];
			if not selfteam.currentSpot == spot and not CS.DeploymentAutoBattleController.SpotHasHardEnemy(spot) then
				if CS.DeploymentAutoBattleController.NeedSupply(selfteam) then
					if CS.DeploymentController.CanSquadSupply(spot) then
						target = spot;
					end
				elseif spot:HasEnemyTeam() then
					target = spot;
				end		
			end
		end
	end
	return target;
end

util.hotfix_ex(CS.DeploymentAutoBattleController,'FindSupplySpotMainTeamAround',FindSupplySpotMainTeamAround)
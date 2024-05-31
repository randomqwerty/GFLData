local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentAutoBattleController)

local FindSupplySpotMainTeamAround = function()
	local spot = CS.DeploymentAutoBattleController.FindSupplySpotMainTeamAround();
	if spot ~= nil then
		return spot;
	end
	local target = nil;
	local currentAutoMoveStep = CS.DeploymentAutoBattleController.currentAutoMoveStep;
	if currentAutoMoveStep:isVehicleTeam() then
		if not CS.DeploymentAutoBattleController.NeedSupply(currentAutoMoveStep.team) then
			local length = 100;
			local spots = currentAutoMoveStep.team.currentSpot:GetSpotInRange(3);
			for i=0,spots.Count-1 do
				local spot = spots[i];
				if spot:HasEnemyTeam() or spot.belong == CS.Belong.enemy then
					local ids = CS.DeploymentAutoBattleController.GenAutoRoute(currentAutoMoveStep.team.currentSpot.spotInfo.id, spot.spotInfo.id, currentAutoMoveStep.team.layer);
					if ids.Count > 0 and ids.Count < length then
						length = ids.Count;
						target = spot;
					end
				end
			end
		end
	end
	return target;
end

util.hotfix_ex(CS.DeploymentAutoBattleController,'FindSupplySpotMainTeamAround',FindSupplySpotMainTeamAround)
local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentAutoBattleController)

local CheckMainTeamAssistTeam = function()
	CS.DeploymentAutoBattleController.CheckMainTeamAssistTeam();
	if CS.DeploymentAutoBattleController.currentAutoMoveStep.teamType == CS.AutoBattleTeamType.MainTeam then
		if CS.DeploymentAutoBattleController.currentMissionSteps ~= nil then
			for i=0,CS.DeploymentAutoBattleController.currentMissionSteps.autoBattleAllSteps.Count-1 do
				local onestep = CS.DeploymentAutoBattleController.currentMissionSteps.autoBattleAllSteps[i];
				if not onestep.onlyOnce then
					CS.DeploymentAutoBattleController.oneStepWaitThisTurn:Remove(onestep.index);
				end
			end
		end
	end
end

util.hotfix_ex(CS.DeploymentAutoBattleController,'CheckMainTeamAssistTeam',CheckMainTeamAssistTeam)
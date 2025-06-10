local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamInfoController)

local ReinforceAllyTeam = function(allyteam,spot)
	if not CS.DeploymentController.isDeplyment then
		for i=0,allyteam.FriendAllyGuns.listGun.Count-1 do
			local gun = allyteam.FriendAllyGuns.listGun[i];
			gun.pos = CS.GF.Battle.GridPos(gun.allyGunInfo.pos25, CS.GF.Battle.GridPos.GridType.grid5x5)
		end
	end
	CS.DeploymentTeamInfoController.ReinforceAllyTeam(allyteam,spot);
end
local CheckAllyFairyAuto = function(allyteam)
	allyteam:UseOriginalGun();
	CS.DeploymentTeamInfoController.CheckAllyFairyAuto(allyteam);
end
util.hotfix_ex(CS.DeploymentTeamInfoController,'ReinforceAllyTeam',ReinforceAllyTeam)
util.hotfix_ex(CS.DeploymentTeamInfoController,'CheckAllyFairyAuto',CheckAllyFairyAuto)
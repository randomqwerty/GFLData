local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamInfoController)

local ReinforceAllyTeam = function(allyteam,spot)
	for i=0,allyteam.FriendAllyGuns.listGun.Count-1 do
		local gun = allyteam.FriendAllyGuns.listGun[i];
		gun.pos = CS.GF.Battle.GridPos(gun.allyGunInfo.pos25, CS.GF.Battle.GridPos.GridType.grid5x5)
	end
	CS.DeploymentTeamInfoController.ReinforceAllyTeam(allyteam,spot);
end

util.hotfix_ex(CS.DeploymentTeamInfoController,'ReinforceAllyTeam',ReinforceAllyTeam)
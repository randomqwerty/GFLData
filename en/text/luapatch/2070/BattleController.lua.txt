local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleController)

local SetLastBattleLeaderGun = function(self)
	if CS.GF.Battle.BattleController.renderTexture == nil then
		self:SetLastBattleLeaderGun();
	end
end
local SetLastBattleEnemyID = function(self)
	if self:CanRecordCurrentSpot() then
		CS.TargetTrainGameData.instance:SetLastBattleEnemyID(self.enemyTeamidUse)
		if CS.BattleUIPauseController.Instance ~= nil then
			CS.BattleUIPauseController.Instance:ShowCollectionBtn()
		end
	end
end

local FinalResult = function(self)
	self:FinalResult();
	for i=0,self.currentSpotAction.battleSquadTeam.Count-1 do
		local squadTeam = self.currentSpotAction.battleSquadTeam[i];
		if squadTeam.sangvisTeam ~= nil then
			local allyTeam = CS.GameData.missionAction.listAllyTeams:GetDataById(squadTeam.sangvisTeam.id);
			if allyTeam ~= nil  and squadTeam.sangvisTeam.friendSquadTeam ~= nil then
				local ammo = CS.Mathf.Max(0, CS.DeploymentController.sangvisCommonSupportAmmo - squadTeam.sangvisTeam.friendSquadTeam.freeBuffAmmo);
				local mre = CS.Mathf.Max(0, CS.DeploymentController.sangvisCommonSupportMre - squadTeam.sangvisTeam.friendSquadTeam.freeBuffMre);
				squadTeam.sangvisTeam.ammo = squadTeam.sangvisTeam.ammo - ammo;
				squadTeam.sangvisTeam.ammo = CS.Mathf.Max(0,squadTeam.sangvisTeam.ammo);
				squadTeam.sangvisTeam.mre = squadTeam.sangvisTeam.mre - mre;
				squadTeam.sangvisTeam.mre = CS.Mathf.Max(0,squadTeam.sangvisTeam.mre);				
			end
		end
	end
end

util.hotfix_ex(CS.GF.Battle.BattleController,'SetLastBattleLeaderGun',SetLastBattleLeaderGun)
util.hotfix_ex(CS.GF.Battle.BattleController,'SetLastBattleEnemyID',SetLastBattleEnemyID)
util.hotfix_ex(CS.GF.Battle.BattleController,'FinalResult',FinalResult)
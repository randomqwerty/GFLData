local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentController)

local RequestNoBattleAllyHandle = function(self,data)
	local json = data.jsonData:GetValue("life_change");
	local keys = CS.System.Collections.Generic.List(CS.System.String)(json.Keys);
	for i=0,keys.Count-1 do
		local temp = json:GetValue(keys[i]);
		if temp:Contains("enemy_hp_percent") then
			local hp = temp:GetValue("enemy_hp_percent").Float;
			local spotid = tonumber(keys[i]);
			local spotaction = CS.GameData.listSpotAction:GetDataById(spotid);
			for j = 0, spotaction.allyTeamInstanceIds.Count-1 do
				local allyteam = CS.GameData.missionAction.listAllyTeams:GetDataById(spotaction.allyTeamInstanceIds[j]);
				allyteam.hpPercent = hp;
			end
		end
	end
	self:RequestNoBattleAllyHandle(data);
end

local TriggerSelectTeam = function(team)
	if team == nil then
		CS.DeploymentBuildSkillItem.showSelectSpot = false;
	end
	CS.DeploymentController.TriggerSelectTeam(team);
end	

local check = false;
local CanPlayerAction = function(self)
	if check then
		return true;
	end
	if CS.GameData.currentSelectedMissionInfo.useDemoMission then
		return false;	
	end
	return true;
end

local ClickSpot = function(self,spot)
	check = true;
	self:ClickSpot(spot);
	check = false;
end

util.hotfix_ex(CS.DeploymentController,'RequestNoBattleAllyHandle',RequestNoBattleAllyHandle)
util.hotfix_ex(CS.DeploymentController,'TriggerSelectTeam',TriggerSelectTeam)
util.hotfix_ex(CS.DeploymentController,'get_CanPlayerAction',CanPlayerAction)
util.hotfix_ex(CS.DeploymentController,'ClickSpot',ClickSpot)




local util = require 'xlua.util'
xlua.private_accessible(CS.MissionAction)

local CheckTeamAfterSkillRes = function(self,jsonData)
	if not CS.Data.IsJsonArrayNull(jsonData) then
		local spotids = CS.System.Collections.Generic.List(CS.System.String)(jsonData.Keys);
		for i=0,spotids.Count-1 do
			local spotid = tonumber(spotids[i]);
			local spotAction = CS.GameData.listSpotAction:GetDataById(spotid);
			local json = jsonData:GetValue(spotids[i]);
			if not CS.Data.IsJsonArrayNull(json) then
				local types = CS.System.Collections.Generic.List(CS.System.String)(json.Keys);
				for j=0,types.Count-1 do
					local temp = json:GetValue(types[j]);
					if spotAction.friendlyTeamId >0 then
						if not CS.Data.IsJsonArrayNull(temp) then
							local ids = CS.System.Collections.Generic.List(CS.System.String)(temp.Keys);
							for m=0,ids.Count-1 do
								local gunid = tonumber(ids[m]);
								local gun = CS.GameData.listGun:GetDataById(gunid);
								gun.ammo = temp:GetValue(ids[m]):GetValue("ammo").Int;
								gun.mre = temp:GetValue(ids[m]):GetValue("mre").Int;
							end
						end
					else
						local ammo = temp:GetValue("ammo").Int;
						local mre = temp:GetValue("mre").Int;
						local energy = temp:GetValue("energy").Int;
						if spotAction.vehicleTeamID >0 then
							local vehicleTeam = CS.GameData.missionAction.listVehicleTeams:GetDataById(spotAction.vehicleTeamID);
							vehicleTeam.vehicle.ammo = ammo;
							vehicleTeam.vehicle.mre = mre;
							vehicleTeam.vehicle.energy = energy;
						end
						if spotAction.sangvisTeamId >0 then
							local sangvisTeam = CS.GameData.dictTeam[spotAction.sangvisTeamId];
							sangvisTeam.ammo = ammo;
							sangvisTeam.mre = mre;
						end
						if spotAction.squadTeamInstanceIds.Count > 0 then
							local squadTeam = CS.GameData.missionAction.listSquadTeams:GetDataById(spotAction.squadTeamInstanceIds[0]);
							squadTeam.squadData.ammo = ammo;
							squadTeam.squadData.mre = mre;
						end
						if spotAction.allyTeamInstanceIds.Count > 0 then
							for i = 0, spotAction.allyTeamInstanceIds.Count-1 do
								local allyTeam = CS.GameData.missionAction.listAllyTeams:GetDataById(spotAction.allyTeamInstanceIds[i]);
								allyTeam.ammo = ammo;
								allyTeam.mre = mre;
								allyTeam.energy = energy;
							end
						end
					end
				end
			end
		end
	end
end
util.hotfix_ex(CS.MissionAction,'CheckTeamAfterSkillRes',CheckTeamAfterSkillRes)

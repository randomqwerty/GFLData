local util = require 'xlua.util'
xlua.private_accessible(CS.MissionAction)


local AnarysicsHurtData = function(self,jsonData)
	self:AnarysicsHurtData(jsonData);
	local teamids = CS.System.Collections.Generic.List(CS.System.Int32)();
	local sangvisteamids = CS.System.Collections.Generic.List(CS.System.Int32)();
	for i=0,CS.GameData.missionAction.queueTeamMove.Count-1 do
		local record = CS.GameData.missionAction.queueTeamMove[i];
		if record.teamId ~= 0 then
			teamids:Add(record.teamId);
		end
		if record.sangvisTeamId ~= 0 then
			sangvisteamids:Add(record.sangvisTeamId);
		end
	end
	for i=0,jsonData.Count -1 do
		local data = jsonData[i];
		local friendTeamId = jsonData[i]:GetValue("team_id").Int;
		local sangvisTeamId = jsonData[i]:GetValue("sangvis_team_id").Int;
		local spotId = jsonData[i]:GetValue("spot_id").Int;
		if friendTeamId >0 and not teamids:Contains(friendTeamId) then
			self:ReadFriendSkillData(friendTeamId,spotId);
		end
		if sangvisTeamId>0 and not sangvisteamids:Contains(sangvisTeamId) then
			self:ReadSangvisSkillData(sangvisTeamId,spotId);
		end
	end 
end
local UseWinCounter = function(self)
	if self.missionInfo.mapped_mission_id ~= 0 then
		local mapInfo = CS.GameData.listMissionMapInfo:GetDataById(self.missionInfo.mapped_mission_id);
		if 	mapInfo == nil then
			return self.winCount;
		end
		local missionids = mapInfo.missionids;
		if missionids.Count==3 then
			local	mission1=CS.GameData.listMission:GetDataById(missionids[1]);
			local	mission2=CS.GameData.listMission:GetDataById(missionids[2]);
			local index = missionids:IndexOf(self.missionInfo.id);
			if index == 1	then
				if mission2.mappedwincounter>0 then
					return self.mappedwincounter;
				end
			elseif index == 0 then
				if mission1.mappedwincounter>0 then
					return self.mappedwincounter;
				end
			end
		end
		if missionids.Count==2 then
			local	mission1=CS.GameData.listMission:GetDataById(missionids[1]);
			local index = missionids:IndexOf(self.missionInfo.id);
			if index == 0	then
				if mission1.mappedwincounter>0 then
					return self.mappedwincounter;
				end
			end
		end	
	end
	return self.winCount;
end
util.hotfix_ex(CS.MissionAction,'AnarysicsHurtData',AnarysicsHurtData)
util.hotfix_ex(CS.Mission,'get_UseWinCounter',UseWinCounter)
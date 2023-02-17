local util = require 'xlua.util'
xlua.private_accessible(CS.MissionAction)


local LoadBattleEnvironment = function(self,jsonData)
	self:LoadBattleEnvironment(jsonData);
	if jsonData:Contains("fight_environment_group") then
		self.environmentTxt=jsonData:GetValue("fight_environment_group").String;
	else
		return;
	end
	local text = Split(self.environmentTxt,"|");
	local iter = self.currentEnvironmentSkill:GetEnumerator();     
	while iter:MoveNext() do                      
		local layer = iter.Current.Key;
        if CS.System.String.IsNullOrEmpty(text[layer+1]) then
			if self.currentEnvironmentSkill:ContainsKey(layer) then
				self.currentEnvironmentSkill[layer]:Clear();
				print("清除enskill"..layer)
			end
		else
			self.currentEnvironmentSkill[layer]:Clear();
			local check = Split(text[layer+1],";");
			for j=1,#check do
				local id = tonumber(check[j]);
				local info = CS.GameData.listBTEnvironmentData:GetDataById(id);
				self.currentEnvironmentSkill[layer]:Add(info);
			end
		end          
	end	
end


function Split(szFullString, szSeparator)
	local nFindStartIndex = 1
	local nSplitIndex = 1
	local nSplitArray = {}
	while true do
		local nFindLastIndex = string.find(szFullString, szSeparator, nFindStartIndex)
		if not nFindLastIndex then
			nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, string.len(szFullString))
			break
		end
		nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, nFindLastIndex - 1)
		nFindStartIndex = nFindLastIndex + string.len(szSeparator)
		nSplitIndex = nSplitIndex + 1
	end
	return nSplitArray
end

local LoadFairySkillPerform = function(self,jsonData,readObject)
	self:LoadFairySkillPerform(jsonData,readObject);
	if readObject then
		local txt1 = jsonData:ToString();
		txt1 = string.gsub(txt1,"\\","");
		jsonData = CS.LitJson.JsonMapper.ToObject(txt1);
	end
	local txt = jsonData:ToJson();
	if txt == "[]" then
		return;
	end
	for i=0,jsonData.Count-1 do
		local sourceType = jsonData[i]:GetValue("source_type").Int;
		local id = jsonData[i]:GetValue("source_value").Int;
		local cd = jsonData[i]:GetValue("next_skill_cd_turn").Int;
		if sourceType == 6 then
			local allyteam = self.listAllyTeams:GetDataById(id);
			if allyteam.currentFairy~=nil then
				allyteam.currentFairy.mainSkill.cdTurn = cd;
			end
		end
	end
end
local LoadKillNum = function(self,jsonData,readObject)
	self:LoadKillNum(jsonData,readObject);
	self:LoadDieEnemy(jsonData,readObject);
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

local isEndless = function(self)
	return self.endlessType ~= 0;
end

local AnarysicsHurtData = function(self,jsonData)
	self:AnarysicsHurtData(jsonData);
	for i=0,jsonData.Count -1 do
		local json = jsonData[i];
		local enemyInstanceId = json:GetValue("enemy_instance_id").Int;
		local spotId = json:GetValue("spot_id").Int;
		local hp = json:GetValue("enemy_hp_percent").Float;
		if enemyInstanceId ~= 0 then
			local oldjson = self.enemyTeamData[enemyInstanceId][spotId];
			local lasthp = oldjson:GetValue("enemy_hp_percent").Float;
			print("lasthp"..lasthp.."hp"..hp);
			if lasthp>hp then
				self.enemyTeamData[enemyInstanceId][spotId] = json;
			end
		end
	end
end
util.hotfix_ex(CS.MissionAction,'LoadBattleEnvironment',LoadBattleEnvironment)
util.hotfix_ex(CS.MissionAction,'LoadFairySkillPerform',LoadFairySkillPerform)
util.hotfix_ex(CS.MissionAction,'LoadKillNum',LoadKillNum)
util.hotfix_ex(CS.Mission,'get_UseWinCounter',UseWinCounter)
util.hotfix_ex(CS.MissionInfo,'get_isEndless',isEndless)
util.hotfix_ex(CS.MissionAction,'AnarysicsHurtData',AnarysicsHurtData)
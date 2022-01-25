local util = require 'xlua.util'
xlua.private_accessible(CS.MissionAction)


local LoadBattleEnvironment = function(self,jsonData)
	self:LoadBattleEnvironment(jsonData);
	local text = Split(self.environmentTxt,"|");
	local iter = self.currentEnvironmentSkill:GetEnumerator();     
	while iter:MoveNext() do                      
		local layer = iter.Current.Key;
        if CS.System.String.IsNullOrEmpty(text[layer]) then
			if self.currentEnvironmentSkill:ContainsKey(layer) then
				self.currentEnvironmentSkill[layer]:Clear();
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
util.hotfix_ex(CS.MissionAction,'LoadBattleEnvironment',LoadBattleEnvironment)
util.hotfix_ex(CS.MissionAction,'LoadFairySkillPerform',LoadFairySkillPerform)
util.hotfix_ex(CS.MissionAction,'LoadKillNum',LoadKillNum)
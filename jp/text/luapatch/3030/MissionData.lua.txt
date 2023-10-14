local util = require 'xlua.util'

local InitData = function(self)	
	self:InitData();
	if not CS.System.String.IsNullOrEmpty(self.limit_team) then
		local txt = Split(self.limit_team,",");
		for j=1,#txt do			
			local mtxt = txt[j];
			if j == 2 then
				if string.find(mtxt, "*") == 1 then	
					mtxt = string.sub(mtxt, 2);
				end	
				self.basetotalTeamLimit	= tonumber(mtxt);
			end
		end
	end
end

local LoadMoveStepData = function(self,jsonData,readAction)
	if  not jsonData:Contains("target_moved_step") then
		return;
	end
	local stepData = jsonData:GetValue("target_moved_step");
	local txt = stepData:ToString();
	if readAction then
		local txt1 = string.gsub(txt,"\\","");
		stepData = CS.LitJson.JsonMapper.ToObject(txt1);
	end
	if CS.Data.IsJsonArrayNull(stepData) then
		return;
	end
	CS.NDebugJson.Log("target_moved_step", stepData);
	self.hasMoveStepData:Clear();
	local turnids = CS.System.Collections.Generic.List(CS.System.String)(stepData.Keys);
	for i=0,turnids.Count-1 do
		local turn = tonumber(turnids[i]);
		if not self.hasMoveStepData:ContainsKey(turn) then
			local data = CS.System.Collections.Generic.Dictionary(CS.MissionAction.TeamMoveStepType,CS.System.Collections.Generic.List(CS.MissionAction.MoveStepData));
			self.hasMoveStepData:Add(turn,data);
		end
		local typeData = stepData:GetValue(turnids[i]);
		if not CS.Data.IsJsonArrayNull(typeData) then
			local types = CS.System.Collections.Generic.List(CS.System.String)(typeData.Keys);
			for j=0,types.Count-1 do
				local moveType = CS.MissionAction.TeamMoveStepType.defult;
				local type = tonumber(types[j]);
				if type == 2 or type == 9 then
					moveType = CS.MissionAction.TeamMoveStepType.friend;
				elseif 	type == 3 or type == 302 or type == 304 then
					moveType = CS.MissionAction.TeamMoveStepType.allyFriend;
				elseif 	type == 4 or type == 5 then
					moveType = CS.MissionAction.TeamMoveStepType.enemy;
				elseif 	type == 6 then
					moveType = CS.MissionAction.TeamMoveStepType.allyOther;
				end
				if not self.hasMoveStepData[turn]:ContainsKey(moveType) then
					self.hasMoveStepData[turn]:Add(moveType,CS.System.Collections.Generic.List(CS.MissionAction.MoveStepData));
				end
				if moveType ~= CS.MissionAction.TeamMoveStepType.defult then
					local temp = typeData:GetValue(types[j]);
					if not CS.Data.IsJsonArrayNull(temp) then
						local ids = CS.System.Collections.Generic.List(CS.System.String)(temp.Keys);
						for m=0,ids.Count-1 do
							local sData = CS.MissionAction.MoveStepData();
							sData.id = tonumber(ids[m]);
							sData.hasMoveStep = temp:GetValue(ids[m]).Int;
							sData.type = type;
							self.hasMoveStepData[turn][moveType]:Add(sData);
						end
					end
				end
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

local LoadSpotaction = function(self,jsonSpotAction)
	local ids = CS.System.Collections.Generic.List(CS.System.Int32)();
	for i=0,jsonSpotAction.Count-1 do
		local id = jsonSpotAction[i]:GetValue("spot_id").Int;
		ids:Add(id);
	end
	for i=0,CS.GameData.listSpotAction.Count-1 do
		local spotaction = CS.GameData.listSpotAction:GetDataByIndex(i);
		if not ids:Contains(spotaction.spotInfo.id) then
			spotaction:EnemyDataClear();
			spotaction.allyTeamInstanceIds:Clear();
		end
	end
	self:LoadSpotaction(jsonSpotAction);
end
util.hotfix_ex(CS.MissionInfo,'InitData',InitData)
util.hotfix_ex(CS.MissionAction,'LoadMoveStepData',LoadMoveStepData)
util.hotfix_ex(CS.MissionAction,'LoadSpotaction',LoadSpotaction)
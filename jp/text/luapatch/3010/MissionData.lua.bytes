local util = require 'xlua.util'
xlua.private_accessible(CS.MissionAction)
--修正数据读取
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
				elseif 	type == 3 or type == 302 then
					moveType = CS.MissionAction.TeamMoveStepType.allyFriend;
				elseif 	type == 4 or type == 5 then
					moveType = CS.MissionAction.TeamMoveStepType.enemy;
				elseif 	type == 6 then
					moveType = CS.MissionAction.TeamMoveStepType.allyOther;	
				end
				if not self.hasMoveStepData[turn]:ContainsKey(moveType) then
					self.hasMoveStepData[turn]:Add(moveType,CS.System.Collections.Generic.List(CS.MissionAction.MoveStepData));
				end	
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

effectdelaytime = 0;
showteam = nil;
showbuild = nil;
local CheckDelay = function()
	CS.DeploymentController.Instance:DelayPlayPerformance(effectdelaytime,nil,true);
	if effectdelaytime>0 then
		local pos = CS.DeploymentBackgroundController.currentLayerData.offset;
		if showteam ~= nil then
			local spot = showteam.currentSpot;
			pos = CS.UnityEngine.Vector2(spot.transform.localPosition.x,spot.transform.localPosition.y);
		elseif showbuild ~= nil then
			local spot = showbuild.spot;
			pos = CS.UnityEngine.Vector2(spot.transform.localPosition.x,spot.transform.localPosition.y);
		end
		CS.DeploymentController.TriggerMoveCameraEvent(pos,true);
	end
	effectdelaytime = 0;
end
local LoadFairySkillReturn = function(self,jsonData,readObject,readHurt,playRightNow)
	self:LoadFairySkillReturn(jsonData,readObject,readHurt,playRightNow);
	print("hurt最大延时"..effectdelaytime);
	if CS.DeploymentController.Instance ~= nil  then
		CS.DeploymentController.Instance:AddInsertPlayPerfomance(CheckDelay);
	end
end
local LoadSkillData = function(self,jsonData,readObject,viewSum,readHurt,playRightNow)	
	self:LoadSkillData(jsonData,readObject,false,readHurt,playRightNow);
end
util.hotfix_ex(CS.MissionAction,'LoadMoveStepData',LoadMoveStepData)
util.hotfix_ex(CS.MissionAction,'LoadFairySkillReturn',LoadFairySkillReturn)
util.hotfix_ex(CS.MissionAction,'LoadSkillData',LoadSkillData)
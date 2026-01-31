local util = require 'xlua.util'
xlua.private_accessible(CS.RequestBuildControl)
xlua.private_accessible(CS.RequestBuffSkillControl)

local SuccessJsonHandleData = function(self,jsonData)
	if jsonData:Contains("spot_act_info") then
		local json = jsonData:GetValue("spot_act_info");
		for i=0,json.Count-1 do
			local spot_id=json[i]:GetValue("spot_id").Int;
			 
			if spot_id==88916 then
				if json[i]:Contains("ally_instance_ids") then

					print("88916 ally_instance_ids")
					local ids=json[i]:GetValue("ally_instance_ids")
					local spotAction = CS.GameData.listSpotAction:GetDataById(spot_id);

					if ids.Count>0 and spotAction~=nil then
						print("88916 Clear ally_instance_ids")
						spotAction.allyTeamInstanceIds:Clear() 
					end
				end 
				break;
			end
		end
	end
	self:SuccessJsonHandleData(jsonData);
end
local BuffSkillSuccessJsonHandleData = function(self,jsonData)
	if jsonData:Contains("fairy_skill_return") then
		local json_1 = jsonData:GetValue("fairy_skill_return");
		if json_1:Contains("allyteam_summoner") then
			local json_2= json_1:GetValue("allyteam_summoner");
			local count = json_2.Count
			for i=0,count-1 do
				local info = json_2[i]:GetValue("ally_instance_info")
				local allyTeamInfoId =info:GetValue("ally_team_id").Int;
				if allyTeamInfoId == 6540013 or allyTeamInfoId == 6540014 or allyTeamInfoId == 6540015 or allyTeamInfoId == 6540016 then
					local spot_id = json_2[i]:GetValue("spot_id").Int;

					local spotAction = CS.GameData.listSpotAction:GetDataById(spot_id);

					if spotAction~=nil then
						print(spot_id.." Clear ally_instance_ids")
						spotAction.allyTeamInstanceIds:Clear() 
					end
				end
			end
		end
		if json_1:Contains("after_charge_rs_change") and  self.mainskill~=nil then
			if self.mainskill.id==770052 or self.mainskill.id==780012 then
				local json_3= json_1:GetValue("after_charge_rs_change");
				if json_3:Contains("ammo") then
					local ammo=json_3:GetValue("ammo").Int;
					CS.GameData.userInfo.ammo = CS.GameData.userInfo.ammo+ammo;
					if CS.GameData.userInfo.ammo<=0 then
						CS.GameData.userInfo.ammo=0;
					end
				end
				if json_3:Contains("mre") then
					local mre=json_3:GetValue("mre").Int;
					CS.GameData.userInfo.mre = CS.GameData.userInfo.mre+mre;
					if CS.GameData.userInfo.mre<=0 then
						CS.GameData.userInfo.mre=0;
					end
				end
			end
		end
	end
	self:SuccessJsonHandleData(jsonData);
end
util.hotfix_ex(CS.RequestBuildControl,'SuccessJsonHandleData',SuccessJsonHandleData)
util.hotfix_ex(CS.RequestBuffSkillControl,'SuccessJsonHandleData',BuffSkillSuccessJsonHandleData)

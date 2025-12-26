local util = require 'xlua.util'
xlua.private_accessible(CS.RequestBuildControl)

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
util.hotfix_ex(CS.RequestBuildControl,'SuccessJsonHandleData',SuccessJsonHandleData)

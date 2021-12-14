local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterExerciseAction)

local InitData  = function(self,data)
	CS.GameData.dicTheaterConstructionActions:Clear();
	if data:Contains("theater_construction_info") then
		local constructionInfos = data:GetValue("theater_construction_info");
		if constructionInfos ~= nil then
			for i=0,constructionInfos.Count-1 do
			    action = CS.TheaterConstructionAction();
				action.construction_group_id = constructionInfos[i]:GetValue("construction_group_id").Int;
                action.lv = constructionInfos[i]:GetValue("lv").Int;
                action.init_pt = constructionInfos[i]:GetValue("init_pt").Int;
                action.pt = constructionInfos[i]:GetValue("pt").Int;
                action.user_pt = constructionInfos[i]:GetValue("user_pt").Int;
                action.theater_id = constructionInfos[i]:GetValue("theater_id").Int;
                CS.GameData.dicTheaterConstructionActions:Add(action.construction_group_id, action);
				
			end
		end
	end
	self:InitData(data);
end

util.hotfix_ex(CS.TheaterExerciseAction,'InitData',InitData)
local util = require 'xlua.util'
xlua.private_accessible(CS.RankingListUIController)

local AnalysisRankData = function(json)
	CS.RankingListUIController.AnalysisRankData(json);
	local jsonuse = json:GetValue("rank_list");
	local type = CS.RankingListUIController.currentListType;
	local order = CS.RankingListUIController.currentDiffcultyOrder;
	for i=0,jsonuse.Count-1 do
		local rank = jsonuse[i]:GetValue("rank").Int;
		local frameid = jsonuse[i]:GetValue("frame_id").Int;
		CS.RankingListUIController.type_Data[type][order].rank_Datas[rank].headFrameId = frameid;
	end
end

util.hotfix_ex(CS.RankingListUIController,'AnalysisRankData',AnalysisRankData)


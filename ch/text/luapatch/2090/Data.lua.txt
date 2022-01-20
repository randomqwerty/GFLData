local util = require 'xlua.util'
xlua.private_accessible(CS.Data)
local myGetFactorScoreFromCommanderRankingScore = function(commanderRankingScore)
	local score = 0;
	if(commanderRankingScore.id == 26 or commanderRankingScore.id == 27 or commanderRankingScore.id == 28 or commanderRankingScore.id == 32 or commanderRankingScore.id == 33 or commanderRankingScore.id == 34) then
		if commanderRankingScore.id == 26 then
			local listSSRSangvis = CS.GameData.listSangvisGun:FindAll(
				function(s)
					return s.basicSangvisTypeData.default_advance_lv == 3 and s.level ~= 1
				end);
			for i = 0, listSSRSangvis.Count - 1 do
				score = score + CS.Data.GetFactorScore(listSSRSangvis[i].level, commanderRankingScore);
			end
			score = score * commanderRankingScore.basic_scores;
			
		end
		if commanderRankingScore.id == 27 then
			local listSSRSangvis = CS.GameData.listSangvisGun:FindAll(
				function(s)
					return s.basicSangvisTypeData.default_advance_lv == 2 and s.level ~= 1
				end);
			for i = 0, listSSRSangvis.Count - 1 do
				score = score + CS.Data.GetFactorScore(listSSRSangvis[i].level, commanderRankingScore);
			end
			score = score * commanderRankingScore.basic_scores;
		end
		if commanderRankingScore.id == 28 then
			local listSSRSangvis = CS.GameData.listSangvisGun:FindAll(
				function(s)
					return s.basicSangvisTypeData.default_advance_lv == 1 and s.level ~= 1
				end);
			for i = 0, listSSRSangvis.Count - 1 do
				score = score + CS.Data.GetFactorScore(listSSRSangvis[i].level, commanderRankingScore);
			end
			score = score * commanderRankingScore.basic_scores;
		end
		if commanderRankingScore.id == 32 then
			local listSSRSangvis = CS.GameData.listSangvisGun:FindAll(
				function(s)
					return s.basicSangvisTypeData.default_advance_lv == 3 and s.level ~= 1
				end);
			for i = 0, listSSRSangvis.Count - 1 do
				score = score + CS.Data.GetFactorScore(listSSRSangvis[i].resolutionLevel, commanderRankingScore);
			end
			score = score * commanderRankingScore.basic_scores;
		end
		if commanderRankingScore.id == 33 then
			local listSSRSangvis = CS.GameData.listSangvisGun:FindAll(
				function(s)
					return s.basicSangvisTypeData.default_advance_lv == 2 and s.level ~= 1
				end);
			for i = 0, listSSRSangvis.Count - 1 do
				score = score + CS.Data.GetFactorScore(listSSRSangvis[i].resolutionLevel, commanderRankingScore);
			end
			score = score * commanderRankingScore.basic_scores;
		end
		if commanderRankingScore.id == 34 then
			local listSSRSangvis = CS.GameData.listSangvisGun:FindAll(
				function(s)
					return s.basicSangvisTypeData.default_advance_lv == 1 and s.level ~= 1
				end);
			for i = 0, listSSRSangvis.Count - 1 do
				score = score + CS.Data.GetFactorScore(listSSRSangvis[i].resolutionLevel, commanderRankingScore);
			end
			score = score * commanderRankingScore.basic_scores;
		end
	else
		score = CS.Data.GetFactorScoreFromCommanderRankingScore(commanderRankingScore)
	end
	return score;
end
util.hotfix_ex(CS.Data,'GetFactorScoreFromCommanderRankingScore',myGetFactorScoreFromCommanderRankingScore)
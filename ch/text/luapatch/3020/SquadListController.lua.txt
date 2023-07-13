local util = require 'xlua.util'
xlua.private_accessible(CS.SquadListController)
xlua.private_accessible(CS.SquadStateRightSideDetailsPanelPresenter)
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

local CheckMissionCanUseSquad = function(self,squads)
	if CS.DeploymentController.Instance ~= nil and not CS.DeploymentController.Instance:isNull() then
		if CS.DailyExploreData.GetInstance() ~= nil then
			if not CS.System.String.IsNullOrEmpty(CS.GameData.currentSelectedMissionInfo.daily_demand) then
				local canuseSquads = CS.System.Collections.Generic.List(CS.Squad)();
				local limmitList = Split(CS.GameData.currentSelectedMissionInfo.daily_demand,"|");
				for i=1,#limmitList do
					local limmitType = Split(limmitList[i],":");
					local type = tonumber(limmitType[1]);
					if type == 2 then
						local limit = Split(limmitType[2],",");
						local squadId = tonumber(limit[1]);
						local star = tonumber(limit[2]);
						local level = tonumber(limit[3]);
						local skillLevel = tonumber(limit[4]);
						for j=0,squads.Count-1 do
							if squads[j].infoId == squadId then
								if CS.DailyExploreData.GetInstance():GetDifficulty() == CS.DailyExploreMissionDifficultyType.Simple then
									if squads[j].level >= level then
										canuseSquads:Add(squads[j]);
									end
								elseif 	CS.DailyExploreData.GetInstance():GetDifficulty() == CS.DailyExploreMissionDifficultyType.Hard then
									if squads[j].level >= level and squads[j].battleSkill1.level >= skillLevel then
										canuseSquads:Add(squads[j]);
									end
								else
									if squads[j].level >= level and squads[j].battleSkill1.level >= skillLevel and squads[j].rank >= star then
										canuseSquads:Add(squads[j]);
									end
								end
							end
						end
					end
				end
				return canuseSquads;
			end
		end
	end
	return squads;
end
local _LevelUp = function(self)
	if  self.squad.fake then

	else
		self:LevelUp();
	end
end
util.hotfix_ex(CS.SquadListController,'CheckMissionCanUseSquad',CheckMissionCanUseSquad)
util.hotfix_ex(CS.SquadStateRightSideDetailsPanelPresenter,'LevelUp',_LevelUp)
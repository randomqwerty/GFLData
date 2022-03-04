local util = require 'xlua.util'

xlua.private_accessible(CS.RankingListUIController)

local ShowAcvitityList = function(self,toogle,order)
	self:ShowAcvitityList(toogle,order);
	self.btnActivity.gameObject:SetActive(false);
	return;
	--if toogle.isOn then
		--local rankInfo = self.showactivityRankInfo[order];
		--local temp = Split(rankInfo.rankSub_type,",");
		--if temp[0] ~= nil then
			--local missionId = tonumber(temp[0]);
			--local missionInfo = CS.GameData.listMissionInfo:GetDataById(missionId);
			--local open = CS.SpecialOPSController.GetOPSOpen().Contains(missionInfo.campaign);
			--self.btnActivity.gameObject:SetActive(open);		
		--end
	--end
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
util.hotfix_ex(CS.RankingListUIController,'ShowAcvitityList',ShowAcvitityList)
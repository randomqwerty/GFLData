local util = require 'xlua.util'
xlua.private_accessible(CS.CommonController)

local QuickJump = function(gotoPageInfo,backAction,customData)
	if gotoPageInfo ~= nil then
		local temp = Split(gotoPageInfo.mGotoSceneInfo,"-");
		if temp[1] == "MissionSelection" then
			CS.MissionSelectionController.recordNormalType = CS.MissionType.normal;
		end
	end
	CS.CommonController.QuickJump(gotoPageInfo,backAction,customData);	
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

util.hotfix_ex(CS.CommonController,'QuickJump',QuickJump)


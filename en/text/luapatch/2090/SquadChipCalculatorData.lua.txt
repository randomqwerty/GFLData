local util = require 'xlua.util'
xlua.private_accessible(CS.SquadChipCalculatorData)

local TryLoadLocalData = function(self,cpuGridID)
	if (not self.DictPatterns:ContainsKey(cpuGridID)) then
		local textAsset = CS.ResManager.GetObjectByPath("ProfilesConfig/Patterns/Patterns_" .. cpuGridID, ".csv")
		if textAsset == nil then
			return
		end
		xlua.cast(textAsset,typeof(CS.UnityEngine.TextAsset)) 
		local emptyList = CS.System.Collections.Generic["List`1[GF.SquadChipCalculator.ChipPattern]"]()
		self.DictPatterns:Add(cpuGridID, emptyList)
		local text = textAsset.text
		local SplitArray = Split(textAsset.text,'\n')
		for i=1,#SplitArray do
			self:ParseString(cpuGridID,SplitArray[i])
		end
	end

end

function Split(szFullString, szSeparator)
	if(szFullString == nil) then
		return nil
	end
	local nFindStartIndex = 0
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
util.hotfix_ex(CS.SquadChipCalculatorData,'TryLoadLocalData',TryLoadLocalData)

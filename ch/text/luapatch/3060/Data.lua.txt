local util = require 'xlua.util'
xlua.private_accessible(CS.Data)

local GetAdjutantSlotPosInfos = function()

	local adjutantConfig = CS.UnityEngine.PlayerPrefs.GetString("localAdjutantSlotPosInfo"); 
	local vecConfigs = Split(adjutantConfig, ",")
	local newConfig = ""

	for i=1, #vecConfigs do
		if vecConfigs[i] == ""then
			local index = i - 1
			newConfig = newConfig ..tostring(index).."||0|False|0_0_0|0_0_0"
		else
			newConfig = newConfig .. vecConfigs[i]
		end

		if i ~= #vecConfigs then        
            newConfig = newConfig .. ","
        end 
	end

	CS.UnityEngine.PlayerPrefs.SetString("localAdjutantSlotPosInfo", newConfig);
	CS.Data.GetAdjutantSlotPosInfos()
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

util.hotfix_ex(CS.Data,'GetAdjutantSlotPosInfos',GetAdjutantSlotPosInfos)



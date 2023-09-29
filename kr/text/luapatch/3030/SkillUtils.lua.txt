local util = require 'xlua.util'

xlua.private_accessible(CS.GF.Battle.SkillUtils)
local FP = CS.TrueSync.FP
local get_hashForceManualGunIdSangvis = function()

	--local _hashForceManualGunIdSangvis = CS.GF.Battle.SkillUtils._hashForceManualGunIdSangvis
	if CS.GF.Battle.SkillUtils._hashForceManualGunIdSangvis == nil then
		--print(tostring(CS.GF.Battle.SkillUtils._hashForceManualGunIdSangvis == nil))
		CS.GF.Battle.SkillUtils._hashForceManualGunIdSangvis = CS.System.Collections.Generic.HashSet(CS.System.Int64)()
		--print(tostring(CS.GF.Battle.SkillUtils._hashForceManualGunIdSangvis == nil))
		if CS.UnityEngine.PlayerPrefs.HasKey("FORCE_MANUAL_CLOSE_DATA_SANGVIS") then
			--print(CS.UnityEngine.PlayerPrefs.GetString("FORCE_MANUAL_CLOSE_DATA_SANGVIS"))
			local sangvisList = Split(CS.UnityEngine.PlayerPrefs.GetString("FORCE_MANUAL_CLOSE_DATA_SANGVIS"),',')	
			for i=1,#sangvisList do	
				if string.len(sangvisList[i]) > 0 then
					local gunid = tonumber(sangvisList[i])
					--print(gunid)
					if(CS.GF.Battle.SkillUtils._hashForceManualGunIdSangvis:Contains(gunid)) then
					
					else
						CS.GF.Battle.SkillUtils._hashForceManualGunIdSangvis:Add(gunid)
					end
				end 
			end
		end
	end
	return CS.GF.Battle.SkillUtils._hashForceManualGunIdSangvis
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
xlua.hotfix(CS.GF.Battle.SkillUtils,'get_hashForceManualGunIdSangvis',get_hashForceManualGunIdSangvis)

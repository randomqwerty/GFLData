local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterCombatSettlementUIController)
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
local myShowTotalScoreNode = function(self,result)
    self:ShowTotalScoreNode(result);
	local adaptive = CS.Data.GetString("theater_adaptive_coef");
	local text = Split(adaptive,",");
	if CS.System.Convert.ToInt32(text[0]) == 0 and CS.System.Convert.ToInt32(text[1]) == 0 then
		self.mAdvantageGunNode:SetActive(false);
	end	
end

local Open = function()
	
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_US then
		local obj = CS.ResManager.GetObjectByPath("UGUIPrefabs/Theater/TheaterCombatSettlement_us");
		local mWndObject = CS.UnityEngine.Object.Instantiate(obj);
		CS.TheaterCombatSettlementUIController.Instance = mWndObject:AddComponent(typeof(CS.TheaterCombatSettlementUIController));
		--CS.TheaterCombatSettlementUIController.OnInstantiate(mWndObject);
		--CS.TheaterCombatSettlementUIController.Open("UGUIPrefabs/Theater/TheaterCombatSettlement_us");		
	else
		local obj = CS.ResManager.GetObjectByPath("UGUIPrefabs/Theater/TheaterCombatSettlement");
		local mWndObject = CS.UnityEngine.Object.Instantiate(obj);
		CS.TheaterCombatSettlementUIController.Instance = mWndObject:AddComponent(typeof(CS.TheaterCombatSettlementUIController));
		--CS.TheaterCombatSettlementUIController.OnInstantiate(mWndObject);
		--CS.TheaterCombatSettlementUIController.Open("UGUIPrefabs/Theater/TheaterCombatSettlement");		
	end
			
end
util.hotfix_ex(CS.TheaterCombatSettlementUIController,'ShowTotalScoreNode',myShowTotalScoreNode)
util.hotfix_ex(CS.TheaterCombatSettlementUIController,'Open',Open)
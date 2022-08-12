local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterCombatSettlementUIController)
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
util.hotfix_ex(CS.TheaterCombatSettlementUIController,'Open',Open)
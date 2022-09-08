local util = require 'xlua.util'
xlua.private_accessible(CS.TheaterCombatSettlementUIController)
local Open = function()
	
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_US then
		local obj = CS.ResManager.GetObjectByPath("UGUIPrefabs/Theater/TheaterCombatSettlement_us2090");
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

local SetLeaderPic = function(self,gun)
	if gun.sangvisInfo ~= nil then
		CS.CommonController.TryLoadEnemyBigPic(gun, self.picLeader);
	else
		CS.CommonController.LoadBigPic(gun, self.picLeader, gun.currentSkinId);
	end
	local rectTrans = self.picLeader:GetComponent(typeof(CS.UnityEngine.RectTransform));
	rectTrans:DOKill();
	rectTrans.localScale = CS.UnityEngine.Vector3(1.5,1.5,1);
	CS.UITweenManager.PlayFadeTweens(rectTrans, 0, 1, 1);
	rectTrans.anchoredPosition3D = CS.UnityEngine.Vector3(1000,-100,0);
	local to = CS.UnityEngine.Vector3(700,-30,0);
	rectTrans:DOAnchorPos3D(to,1):Play();
end
util.hotfix_ex(CS.TheaterCombatSettlementUIController,'Open',Open)
util.hotfix_ex(CS.TheaterCombatSettlementUIController,'SetLeaderPic',SetLeaderPic)
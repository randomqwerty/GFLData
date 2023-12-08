local util = require 'xlua.util'
xlua.private_accessible(CS.HomeController)
xlua.private_accessible(CS.ServerInfo)
xlua.private_accessible(CS.GameData)
xlua.private_accessible(CS.UserRecord)
--xlua.private_accessible(CS.CommonGuideController)
xlua.private_accessible(CS.HomeOperationButton)
xlua.private_accessible(CS.NavigationController)
local mySevenLoginCheck = function(self)
	--print(CS.GameData.userRecord._bpBuyCount)
	if CS.GameData.userRecord ~= nil and CS.GameData.userRecord._bpBuyCount==0 then
		CS.GameData.userRecord._bpBuyCount = CS.GameData.userRecord._bpBuyCount+1;
		CS.GameData.ClearPurchaseGoods();
		CS.ServerInfo.Instance:RequestProductList(
			function ()
				CS.ConnectionController.CloseConsole(); 
			end
		);
		--先 跳过日常 玩法新手
		-- if CS.CommonGuideController.Instance~=nil and CS.CommonGuideController.Instance.arrGuideStatus.Length>185 then
		-- 	CS.CommonGuideController.Instance.arrGuideStatus[180]=true;
		-- 	CS.CommonGuideController.Instance.arrGuideStatus[183]=true;
		-- 	CS.CommonGuideController.Instance.arrGuideStatus[184]=true;
		-- 	CS.CommonGuideController.Instance.arrGuideStatus[185]=true;
		-- end
		if CS.NavigationController.ExistInstance then
			CS.NavigationController.isInistanceItem=false;
			CS.Utility.Destroy(CS.NavigationController.Instance.gameObject);
		end
	end
    self:SevenLoginCheck()
end
local _Start = function(self)
	self:Start()
	local seven = CS.Data.GetInt("anniversary_guns_avg_switch");
	if seven ~=0 then
		local obj = self.transform:Find("HomeTalk(Clone)");
		if obj ~=nil then
			obj:SetParent(self.transform.parent, false);
			obj:SetAsFirstSibling();
			self.transform.parent:GetComponent(typeof(CS.UnityEngine.RectTransform)).sizeDelta = CS.UnityEngine.Vector2(1442,155);
		end
	end
end
util.hotfix_ex(CS.HomeOperationButton,'Start',_Start)
util.hotfix_ex(CS.HomeController,'SevenLoginCheck',mySevenLoginCheck)
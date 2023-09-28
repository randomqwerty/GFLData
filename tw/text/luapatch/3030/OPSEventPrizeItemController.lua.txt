local util = require 'xlua.util'
xlua.private_accessible(CS.OPSEventPrizeItemController)
xlua.private_accessible(CS.DWRewardBoxCtrl)

local ShowPackageReward = function(self,package)
	local obj =  CS.UnityEngine.Object.Instantiate(CS.ResManager.GetObjectByPath("UGUIPrefabs/Quests/RewardsViewer"));
	obj:GetComponent(typeof(CS.UnityEngine.Canvas)).sortingOrder = 60;
	obj.transform:SetParent(CS.CommonController.MainCanvas.transform, false);
	local rewardBoxCtrl = obj:GetComponent(typeof(CS.DWRewardBoxCtrl));
	rewardBoxCtrl:Close();
	rewardBoxCtrl:ShowPackagePrize(package);	
end 
local Close = function(self)
	self:Close();
	if self.iconList.Count >0 and CS.Utility.loadedLevelName ~= "Quests" then
		CS.Utility.Destroy(self.gameObject);
	end
end 
util.hotfix_ex(CS.OPSEventPrizeItemController,'ShowPackageReward',ShowPackageReward)
util.hotfix_ex(CS.DWRewardBoxCtrl,'Close',Close)

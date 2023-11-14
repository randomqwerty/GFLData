local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBackgroundController)

local HideMap = function(self,clearteam)
	self.gameObject:SetActive(false);
	self.transform:GetChild(0).gameObject:SetActive(false);
	self.transform:GetChild(1).gameObject:SetActive(false);
	local friendParent = self.transform:Find("Active/Friendly");
	local enemyParent = self.transform:Find("Active/Enemy");
	local lineParent = self.transform:Find("Active/MoveLines");
	friendParent:DestroyChildren(true);
	enemyParent:DestroyChildren(true);
	lineParent:DestroyChildren(true);
	for i=0,self.listSpot.Count-1 do
		local spot = self.listSpot:GetDataByIndex(i);
		spot:CleanMask();
		if clearteam then
			if spot.buildControl ~= nil then
				CS.UnityEngine.Object.DestroyImmediate(spot.buildControl.gameObject);
				spot.buildControl = nil;
			end
		end
	end
end


util.hotfix_ex(CS.DeploymentBackgroundController,'HideMap',HideMap)

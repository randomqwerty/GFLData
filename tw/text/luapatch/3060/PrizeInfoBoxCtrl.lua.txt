local util = require 'xlua.util'
xlua.private_accessible(CS.PrizeInfoBoxCtrl)

local mCreateIcons = function(self)
	self:CreateIcons();

	if self.package ~= nil and self.package.listSangvisGunInfo.Count > 0 then
		for i=0,self.package.listSangvisGunInfo.Count-1 do

			local icon = self.package:GetIconBuilder():SetDestroyUnused(false):SetTitle(self.package.listSangvisGunInfo[i].name):SetSangvisGun(self.package.listSangvisGunInfo[i]):Build():GetComponent(typeof(CS.CommonIconController));
			local bundleIcon = CS.UnityEngine.Object.Instantiate(self.BaseItem);
			bundleIcon.transform:SetParent(self.listHolder, false);
			bundleIcon:Init(icon);
			icon.goStars:SetActive(false);
            icon:SetRewardItemNumber("1");	
		end
	end
end
util.hotfix_ex(CS.PrizeInfoBoxCtrl,'CreateIcons',mCreateIcons)



local util = require 'xlua.util'
xlua.private_accessible(CS.CombineController)

local _CombinePreviewMreAnimation = function(self)
	if self.oldMre > 0 and self.oldMre < self.mainGunItem.gun.maxMre then
		self.tweenCombinePreviewAmmo.NumberFrom = self.oldMre;
            self.tweenCombinePreviewAmmo.NumberTo = self.mainGunItem.gun.maxMre;
            --self.tweenCombinePreviewAmmo.DOKill(false);
            self.tweenCombinePreviewAmmo:Play();
	end
end
local _CombinePreviewAmmoAnimation = function(self)
	if self.oldAmmo > 0 and self.oldAmmo < self.mainGunItem.gun.maxAmmo then
		self.tweenCombinePreviewMre.NumberFrom = self.oldAmmo;
            self.tweenCombinePreviewMre.NumberTo = self.mainGunItem.gun.maxAmmo;
            --self.tweenCombinePreviewMre.DOKill(false);
            self.tweenCombinePreviewMre:Play();
	end
end
util.hotfix_ex(CS.CombineController,'CombinePreviewMreAnimation',_CombinePreviewMreAnimation)
util.hotfix_ex(CS.CombineController,'CombinePreviewAmmoAnimation',_CombinePreviewAmmoAnimation)



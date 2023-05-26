local util = require 'xlua.util'
xlua.private_accessible(CS.CommonGetNewSangvisGunController)

local InitSangvisGunInfo = function(self,sangvisGun,action)
	self:InitSangvisGunInfo(sangvisGun,action);
	if self.imgBoss.transform.childCount>0 then
		local pic = self.imgBoss.transform:GetChild(0):GetComponent(typeof(CS.CommonPicController));
		if pic ~= nil then
			pic:SwitchDamaged(false);
		end
	end
end
util.hotfix_ex(CS.CommonGetNewSangvisGunController,'InitSangvisGunInfo',InitSangvisGunInfo)
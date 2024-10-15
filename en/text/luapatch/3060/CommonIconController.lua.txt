local util = require 'xlua.util'
xlua.private_accessible(CS.CommonIconController.CommonIconControllerBuilder)

local SetSangvisGun = function(self,sangvisGunInfo)
	if sangvisGunInfo ~= nil then
		self:AddOrSetValue("introduction", CS.System.String.Format(CS.Data.GetLang(260162), sangvisGunInfo.name))
	end
	return self:SetSangvisGun(sangvisGunInfo)
end

util.hotfix_ex(CS.CommonIconController.CommonIconControllerBuilder,'SetSangvisGun',SetSangvisGun)


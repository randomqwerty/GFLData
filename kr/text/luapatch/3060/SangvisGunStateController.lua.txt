local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisGunStateController)

local UpdateBasePlateUI = function(self)
	if self.picController ~= nil and self.picController:GetType() == typeof(CS.SangvisSmallPicController) then
		self.basePlate:SetActive(true)
	end
end


util.hotfix_ex(CS.SangvisGunStateController,'UpdateBasePlateUI',UpdateBasePlateUI)





local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisGunStateController)

local mShowGunNumber = function(self)
	self:ShowGunNumber();
	if self.bookGunInfo ~= nil then
		if self.bookGunInfo.isAdditional == true and self.bookGunInfo.id > 100010 then
			local id = 	self.bookGunInfo.id - 100010
			self.textGunNember.text = id.."";
		end
	end
end
util.hotfix_ex(CS.SangvisGunStateController,'ShowGunNumber',mShowGunNumber)

local util = require 'xlua.util'
xlua.private_accessible(CS.FactoryResourceController)
xlua.private_accessible(CS.WishGunEventBoxController)

 
local mBatchDevelop = function(self)
	if self.eventInfo~=nil then
		if self.eventInfo.develop_type==1 then
			CS.FactoryResourceController.type = CS.DevelopType.Gun;
		else
			CS.FactoryResourceController.type = CS.DevelopType.SpecialGun;
		end
	end
	--print(CS.FactoryResourceController.type)
	self:BatchDevelop();
end
util.hotfix_ex(CS.WishGunEventBoxController,'BatchDevelop',mBatchDevelop)
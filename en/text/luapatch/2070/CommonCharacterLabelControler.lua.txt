local util = require 'xlua.util'
xlua.private_accessible(CS.CommonCharacterLabelControler)

local UpdateSangvisInfo = function(self,sangvisGun)
	if sangvisGun == nil then
		self.goNormal:SetActive(false);
		self.goEmpty:SetActive(true);
		return;
	end
	self:UpdateSangvisInfo(sangvisGun);	
end
util.hotfix_ex(CS.CommonCharacterLabelControler,'UpdateSangvisInfo',UpdateSangvisInfo)


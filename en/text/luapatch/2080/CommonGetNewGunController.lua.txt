local util = require 'xlua.util'
xlua.private_accessible(CS.CommonGetNewGunController)
xlua.private_accessible(CS.WishGunEventBoxController)
local isAboveWish = false
local myStart = function(self)
	isAboveWish = CS.WishGunEventBoxController.Instance ~= nil and CS.WishGunEventBoxController.Instance.gameObject.activeSelf;
	if isAboveWish then
		CS.WishGunEventBoxController.Instance:Close();
	end
	self:Start()
end
local myClose = function(self)
	if self.boolCanClose and isAboveWish then
		CS.FactoryController.Instance:SetBtnCancel(true, 
			function ()
				CS.WishGunEventBoxController.Instance:Close();
				end
			);
		CS.WishGunEventBoxController.Instance.gameObject:SetActive(true);
		CS.WishGunEventBoxController.Instance:InitWithData(CS.WishGunEventBoxController.Instance.eventType);
	end
	self:Close();
end

util.hotfix_ex(CS.CommonGetNewGunController,'Start',myStart)
util.hotfix_ex(CS.CommonGetNewGunController,'Close',myClose)
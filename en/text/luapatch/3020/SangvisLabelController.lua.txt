local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisLabelController)

local CheckBtnSwitchGun = function(self,showCanSwitch,showClock)
	self:CheckBtnSwitchGun(showCanSwitch,showClock);
	if self.gun == nil then
		self.imageSwitchClock.gameObject:SetActive(false);
		self.btnSwitchGun.gameObject:SetActive(false);
	end
end

util.hotfix_ex(CS.SangvisLabelController,'CheckBtnSwitchGun',CheckBtnSwitchGun)
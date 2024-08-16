local util = require 'xlua.util'
xlua.private_accessible(CS.EquipGroupProgressLable)

local mShowGroupUI = function(self)
	if self.gun ~=null and self.isIllustratedBookState==false then
		if self.gun.status == CS.GunStatus.mission or self.gun.status == CS.GunStatus.operation  then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(100028));
			return;
		end 
	end
	self:ShowGroupUI();
end

util.hotfix_ex(CS.EquipGroupProgressLable,'ShowGroupUI',mShowGroupUI)
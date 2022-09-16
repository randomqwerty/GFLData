local util = require 'xlua.util'
xlua.private_accessible(CS.FormationEquipLabelController)
xlua.private_accessible(CS.GunStateController)
xlua.private_accessible(CS.GunStateRightSideController)
xlua.private_accessible(CS.GunStateEquipmentController)
local _Awake = function(self)
	self:Awake();
	if self.arrImageRankBackground~=nil and self.arrImageRankBackground.Length==0 and CS.GunStateController.Instance~=nil and CS.GunStateController.Instance.mRightController.EquipmentController~=nil then
		
		if CS.GunStateController.Instance.mRightController.EquipmentController.arrEquipLabel[0].arrImageRankBackground.Length>0 then
			self.arrImageRankBackground=CS.GunStateController.Instance.mRightController.EquipmentController.arrEquipLabel[0].arrImageRankBackground;
		end
		print(self.SlotID);
	end 
end
util.hotfix_ex(CS.FormationEquipLabelController,'Awake',_Awake)
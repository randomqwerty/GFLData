local util = require 'xlua.util'
xlua.private_accessible(CS.GunStateController)

local OnClickBack = function(self)
	if self.equipmoving == false and self.currentLoadLevel == CS.LoadLevel.FormationHold and CS.TheaterEchelonSelection.Instance ~= nil
	 and CS.UISimulatorFormation.isExist == true and CS.CommonCharacterListController.Instance ~= nil then
		CS.UISimulatorFormation.Instance:SangvisGunPagination(true,false);
	end
	self:OnClickBack();
	if CS.TheaterEchelonSelection.Instance ~= nil then
		if CS.CommonCharacterListController.Instance == nil or CS.CommonCharacterListController.Instance.gameObject.activeInHierarchy == false then
		CS.TheaterEchelonSelection.Instance:CloseTopUI();
		end
		CS.TheaterEchelonSelection.Instance:RefreshBossScore();
	end
end
util.hotfix_ex(CS.GunStateController,'OnClickBack',OnClickBack)
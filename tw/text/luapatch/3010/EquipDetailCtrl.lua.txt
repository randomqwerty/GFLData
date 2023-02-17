local util = require 'xlua.util'
xlua.private_accessible(CS.IllusBookEquipSuitCtrl)
xlua.private_accessible(CS.CommonCharacterListLabelControlerNew)
xlua.private_accessible(CS.CommonSceneManagerController)
--xlua.private_accessible(CS.EquipInfo)
local _Open = function(self) 
	print(self.canSelectBtn);
end
local _loadEquipInGun = function(self) 
	xlua.hotfix(CS.CommonCharacterListLabelControlerNew,'Open',_Open)
	self:loadEquipInGun(); 
	if self.gunLable~=nil then
		self.gunLable.canSelectBtn=false;
	end
	
end
local _CloseUI = function(self) 
	xlua.hotfix(CS.CommonCharacterListLabelControlerNew,'Open',nil)
	self:CloseUI(); 
end
local myCheckBtnActive = function(self) 
	if(CS.CommonSceneManagerController.instance.currentSceneName == "Formation" or CS.CommonSceneManagerController.instance.currentSceneName == "StoreRoom" or CS.CommonSceneManagerController.instance.currentSceneName == "Theater") then
		if self.equipInfo.canStrengthen == false then
			if self.leftStrengthBtn.gameObject.activeSelf then
				self.leftStrengthBtn.gameObject:SetActive(false);
			end
		end
	else
		self:CheckBtnActive();
	end
end
util.hotfix_ex(CS.EquipDetailCtrl,'loadEquipInGun',_loadEquipInGun)
util.hotfix_ex(CS.EquipDetailCtrl,'CloseUI',_CloseUI)
util.hotfix_ex(CS.EquipDetailCtrl,'CheckBtnActive',myCheckBtnActive)


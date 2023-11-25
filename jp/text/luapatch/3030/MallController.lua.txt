local util = require 'xlua.util'
xlua.private_accessible(CS.MallController)
xlua.private_accessible(CS.VehicleGoodItemCtrl)
xlua.private_accessible(CS.MallSkinDisplayItemListController)
xlua.private_accessible(CS.ClothesStoreController)
xlua.private_accessible(CS.WareHouseListController)

local _JumpToTab = function(self,jumpType)
	if jumpType == 3 then
		self:OnClickMilitary(true, CS.MallGoodClassification.Military);
	elseif jumpType == 6 then
		self:OnClickExchange(true, CS.MallGoodClassification.Exchange);
	elseif jumpType == 7 then
		self:OnClickSpecialSupply(false, CS.MallGoodClassification.SpecialSupply_MonthCard);
	elseif jumpType == 8 then
		self:OnClickSpecialSupply(false, CS.MallGoodClassification.SpecialSupply_Daily);
	elseif jumpType == 9 then
		self:OnClickSpecialSupply(false, CS.MallGoodClassification.SpecialSupply_Other);
	elseif jumpType == 10 then
		self:OnClickGiftPackage(false, CS.MallGoodClassification.Gift_Pass);
	end
	self:JumpToTab(jumpType);
end
local _InitSkinID = function(self)
	self:InitSkinID();

	if self.skin_info ~=nil then
		self.strTitle = self.skin_info.Name;
		self.strIntroduction = self.skin_info.Introduce;
	end
	if self.tex_TypeName.text.color.r < 0.9 then
		self.tex_TypeName.text.color=CS.UnityEngine.Color(1,1,1,1);
	end
end
local _SetName = function(self)
	self:SetName();

	if self.skin_info ~=nil and self.skin_info.type == 1 then
		
		local id = self.skin_info.VehilceID;
		if id>0 and CS.GameData.listVehicleData:ContainsKey(id) then
			if self.tex_TypeName.gameObject.activeSelf == false then
				self.tex_TypeName.gameObject:SetActive(true);
			end
			local name = CS.GameData.listVehicleData:GetDataById(id).Name;
			self.tex_TypeName:SetText(name);
		end
	end
	
end
local _InitData = function(self)
	if CS.MallController.Instance ~=nil and CS.MallController.Instance.listSkinTheme ~=nil and CS.MallController.Instance.listSkinTheme:Contains(0) then
		CS.MallController.Instance.listSkinTheme:Remove(0);
	end
	self:InitData();
end
local clothInitUIElements = function(self)
	 self.effectsLayout.needRestPivotY=true;
end
local clothSynchronizeData = function(self,type)
	if self.effectDataSource == nil then 
		self.effectDataSource = CS.GameData.userCommanderEffectList;
	end 
	self.SynchronizeData(type);
end
util.hotfix_ex(CS.MallController,'JumpToTab',_JumpToTab)
util.hotfix_ex(CS.VehicleGoodItemCtrl,'InitSkinID',_InitSkinID)
util.hotfix_ex(CS.VehicleGoodItemCtrl,'SetName',_SetName)
util.hotfix_ex(CS.MallSkinDisplayItemListController,'InitData',_InitData)
util.hotfix_ex(CS.ClothesStoreController,'InitUIElements',clothInitUIElements)
util.hotfix_ex(CS.WareHouseListController,'SynchronizeData',clothSynchronizeData)
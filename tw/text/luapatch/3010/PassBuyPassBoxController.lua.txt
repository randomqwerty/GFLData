local util = require 'xlua.util'
xlua.private_accessible(CS.PassBuyPassBoxController)
xlua.private_accessible(CS.PassOrderUserData)
xlua.private_accessible(CS.HotUpdateController)
xlua.private_accessible(CS.GameData)
xlua.private_accessible(CS.Data)
local myRefreshPriceLabel = function(self)
    self:RefreshPriceLabel()
	local normal1 = self.normalPassBuyPrice_Obj.transform:GetChild(0);
	if normal1 ~= nil then
		normal1.gameObject:SetActive(false);
	end
	local normal2 = self.normalDiscountPrice_Obj.transform:GetChild(0);
	if normal2 ~= nil then
		normal2.gameObject:SetActive(false);
	end
	local normal3 = self.normalDiscountPrice_Obj.transform:GetChild(2);
	if normal3 ~= nil then
		normal3.gameObject:SetActive(false);
	end
	
	local deluxe1 = self.deluxePassBuyPrice_Obj.transform:GetChild(0);
	if deluxe1 ~= nil then
		deluxe1.gameObject:SetActive(false);
	end
	local deluxe2 = self.deluxeDiscountPrice_Obj.transform:GetChild(0);
	if deluxe2 ~= nil then
		deluxe2.gameObject:SetActive(false);
	end
	local deluxe3 = self.deluxeDiscountPrice_Obj.transform:GetChild(2);
	if deluxe3 ~= nil then
		deluxe3.gameObject:SetActive(false);
	end
	
	if CS.PassOrderUserData.Instance.normalGood ~= nil then
			if self.currentOrder.enjoyDiscount == true then
				if CS.PassOrderUserData.Instance:UnlockLevel(self.currentOrder.id) == CS.PassOrderUserData.PassOrderUnLockType.PassOrderUnLockTypeNone then
					self.normalPassBuyPrice_Obj:SetActive(false);
					self.deluxePassBuyPrice_Obj:SetActive(false);
					self.normalDiscountPrice_Obj:SetActive(true);
					self.deluxeDiscountPrice_Obj:SetActive(true);
					local normalPrice = "";
					if (CS.System.String.IsNullOrEmpty(CS.PassOrderUserData.Instance.normalGood.displayPrice)) then
						normalPrice = CS.Data.GetLang(71011) .. CS.PassOrderUserData.Instance.normalGood.pointPrice;
					else
						normalPrice = CS.PassOrderUserData.Instance.normalGood.displayPrice;
					end
					self.normalDiscountBuyPrice_Tex.text = normalPrice;
					local normalDiscountPrice = "";
					if (CS.System.String.IsNullOrEmpty(CS.PassOrderUserData.Instance.normalDiscountGood.displayPrice)) then
						normalDiscountPrice = CS.Data.GetLang(71011) .. CS.PassOrderUserData.Instance.normalDiscountGood.pointPrice;
					else
						normalDiscountPrice = CS.PassOrderUserData.Instance.normalDiscountGood.displayPrice;
					end
					self.normalDiscountBuyPriceNow_Tex.text = normalDiscountPrice;
					local deluxeDiscountPrice = "";
					if (CS.System.String.IsNullOrEmpty(CS.PassOrderUserData.Instance.spGood.displayPrice)) then
						deluxeDiscountPrice = CS.Data.GetLang(71011) .. CS.PassOrderUserData.Instance.spGood.pointPrice;
					else
						deluxeDiscountPrice = CS.PassOrderUserData.Instance.spGood.displayPrice;
					end
					self.deluxeDiscountBuyPrice_Tex.text = deluxeDiscountPrice;
					local deluxeDiscountNowPrice = "";
					if (CS.System.String.IsNullOrEmpty(CS.PassOrderUserData.Instance.spDiscountGood.displayPrice)) then
						deluxeDiscountNowPrice = CS.Data.GetLang(71011) .. CS.PassOrderUserData.Instance.spDiscountGood.pointPrice;
					else
						deluxeDiscountNowPrice = CS.PassOrderUserData.Instance.spDiscountGood.displayPrice;
					end
					self.deluxeDiscountBuyPriceNow_Tex.text = deluxeDiscountNowPrice;				
				elseif CS.PassOrderUserData.Instance:UnlockLevel(self.currentOrder.id) == CS.PassOrderUserData.PassOrderUnLockType.PassOrderUnLockTypeBasic then
					self.normalPassBuyPrice_Tex.text = "";
					self.normalPassBuyImgObj:SetActive(true);
					local deluxeDiscountNowPrice = "";
					if (CS.System.String.IsNullOrEmpty(CS.PassOrderUserData.Instance.spDiscountSupplyGood.displayPrice)) then
						deluxeDiscountNowPrice = CS.Data.GetLang(71011) .. CS.PassOrderUserData.Instance.spDiscountSupplyGood.pointPrice;
					else
						deluxeDiscountNowPrice = CS.PassOrderUserData.Instance.spDiscountSupplyGood.displayPrice;
					end
					self.deluxePassBtn_BuyPrice_Tex.text = deluxeDiscountNowPrice;
				else	
					self.normalPassBuyImgObj:SetActive(true);
					self.deluxPassBuyImgObj:SetActive(true);	
				end
			else
				if CS.PassOrderUserData.Instance:UnlockLevel(self.currentOrder.id) == CS.PassOrderUserData.PassOrderUnLockType.PassOrderUnLockTypeNone then
					local normalPassPrice = "";
					if (CS.System.String.IsNullOrEmpty(CS.PassOrderUserData.Instance.normalGood.displayPrice)) then
						normalPassPrice = CS.Data.GetLang(71011) .. CS.PassOrderUserData.Instance.normalGood.pointPrice;
					else
						normalPassPrice = CS.PassOrderUserData.Instance.normalGood.displayPrice;
					end
					self.normalPassBuyPrice_Tex.text = normalPassPrice;
					local deluxePassPrice = "";
					if (CS.System.String.IsNullOrEmpty(CS.PassOrderUserData.Instance.spGood.displayPrice)) then
						deluxePassPrice = CS.Data.GetLang(71011) .. CS.PassOrderUserData.Instance.spGood.pointPrice;
					else
						deluxePassPrice = CS.PassOrderUserData.Instance.spGood.displayPrice;
					end
					self.deluxePassBtn_BuyPrice_Tex.text = deluxePassPrice;				
				elseif CS.PassOrderUserData.Instance:UnlockLevel(self.currentOrder.id) == CS.PassOrderUserData.PassOrderUnLockType.PassOrderUnLockTypeBasic then
					self.normalPassBuyPrice_Tex.text = "";
					self.normalPassBuyImgObj:SetActive(true);
					local deluxePassPrice = "";
					if (CS.System.String.IsNullOrEmpty(CS.PassOrderUserData.Instance.spSupplyGood.displayPrice)) then
						deluxePassPrice = CS.Data.GetLang(71011) ..  CS.PassOrderUserData.Instance.spSupplyGood.pointPrice;
					else
						deluxePassPrice = CS.PassOrderUserData.Instance.spSupplyGood.displayPrice;
					end
					self.deluxePassBtn_BuyPrice_Tex.text = deluxePassPrice;
				else			
					self.normalPassBuyImgObj:SetActive(true);
					self.deluxPassBuyImgObj:SetActive(true);
				end		
			end
	end											
end
local myCheckAndCreateGood = function(self)
	CS.ConnectionController.CloseConsole();
	myRefreshPriceLabel(self);
end
local myOnIAPValidateComplete = function(self)
	--self:OnIAPValidateComplete();
	CS.ConnectionController.CloseConsole();
	myRefreshPriceLabel(self);
	self.normalPassBuy_Btn.onClick:RemoveAllListeners();
	self.normalPassBuy_Btn:AddOnClick(function()
		self:BuyPassOrder(true);
		end);
	self.deluxePassBtn_Buy_Btn.onClick:RemoveAllListeners();
    self.deluxePassBtn_Buy_Btn:AddOnClick(function()
		self:BuyPassOrder(false);
		end);
end
local myStart = function(self)
	--print("myStart");
	-- for i=CS.GameData.listMallGood.Count - 1, 0, -1 do
	-- 	if CS.GameData.listMallGood[i].type == CS.GoodType.payToPassOrder then
	-- 		print("Remove one");
	-- 		CS.GameData.listMallGood:RemoveAt(i);
	-- 	end
	-- end
	local order = CS.PassOrderUserData.Instance:HasActivePassOrder();
	local rmbid0 = order.productArr[0].."";
	local rmbid1 = order.productArr[1].."";
	local rmbid2 = order.productArr[2].."";
	--local list_int= CS.System.Collections.Generic.List(CS.System.Int32)();
	for i=CS.GameData.listMallGood.Count - 1, 0, -1 do
		if CS.GameData.listMallGood[i].rmbId== rmbid0 or CS.GameData.listMallGood[i].rmbId== rmbid1 or CS.GameData.listMallGood[i].rmbId== rmbid2 then
			print("rmb Remove one");
			CS.GameData.listMallGood:RemoveAt(i);
		end
	end
	self:Start();
	self.normalPassBuy_Btn.onClick:RemoveAllListeners();
	self.deluxePassBtn_Buy_Btn.onClick:RemoveAllListeners();
	--self:RequestMallGood();
end
if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then

	util.hotfix_ex(CS.PassBuyPassBoxController,'RefreshPriceLabel',myRefreshPriceLabel)
	util.hotfix_ex(CS.PassBuyPassBoxController,'CheckAndCreateGood',myCheckAndCreateGood)
	util.hotfix_ex(CS.PassBuyPassBoxController,'OnIAPValidateComplete',myOnIAPValidateComplete)
	util.hotfix_ex(CS.PassBuyPassBoxController,'Start',myStart)
end

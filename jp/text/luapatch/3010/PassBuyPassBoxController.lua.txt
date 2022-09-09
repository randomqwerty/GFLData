local util = require 'xlua.util'
xlua.private_accessible(CS.PassBuyPassBoxController)
xlua.private_accessible(CS.PassOrderUserData)
xlua.private_accessible(CS.HotUpdateController)
xlua.private_accessible(CS.GameData)
local myRefreshPriceLabel = function(self)
	print("===")
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
					self.normalDiscountBuyPrice_Tex.text = self.PassOrderUserData.Instance.normalGood.displayPrice:ToString();
					self.normalDiscountBuyPriceNow_Tex.text = self.PassOrderUserData.Instance.normalDiscountGood.displayPrice:ToString();
					self.deluxeDiscountBuyPrice_Tex.text = self.PassOrderUserData.Instance.spGood.displayPrice:ToString();
					self.deluxeDiscountBuyPriceNow_Tex.text = self.PassOrderUserData.Instance.spDiscountGood.displayPrice:ToString();
				elseif CS.PassOrderUserData.Instance:UnlockLevel(self.currentOrder.id) == CS.PassOrderUserData.PassOrderUnLockType.PassOrderUnLockTypeBasic then
					self.normalPassBuyPrice_Tex.text = "";
					self.normalPassBuyImgObj:SetActive(true);
					self.deluxePassBtn_BuyPrice_Tex.text = CS.PassOrderUserData.Instance.spDiscountSupplyGood.displayPrice:ToString();
				else	
					self.normalPassBuyImgObj:SetActive(true);
					self.deluxPassBuyImgObj:SetActive(true);	
				end
			else
				if CS.PassOrderUserData.Instance:UnlockLevel(self.currentOrder.id) == CS.PassOrderUserData.PassOrderUnLockType.PassOrderUnLockTypeNone then
					self.normalPassBuyPrice_Tex.text = CS.PassOrderUserData.Instance.normalGood.displayPrice:ToString();
					self.deluxePassBtn_BuyPrice_Tex.text = CS.PassOrderUserData.Instance.spGood.displayPrice:ToString();
				elseif CS.PassOrderUserData.Instance:UnlockLevel(self.currentOrder.id) == CS.PassOrderUserData.PassOrderUnLockType.PassOrderUnLockTypeBasic then
					self.normalPassBuyPrice_Tex.text = "";
					self.normalPassBuyImgObj:SetActive(true);
					self.deluxePassBtn_BuyPrice_Tex.text = CS.PassOrderUserData.Instance.spSupplyGood.displayPrice:ToString();
				else			
					self.normalPassBuyImgObj:SetActive(true);
					self.deluxPassBuyImgObj:SetActive(true);
				end		
			end
	end											
end
local myOnIAPValidateComplete = function(self)
	self:OnIAPValidateComplete();
	myRefreshPriceLabel(self);
end
local myStart = function(self)
	for i=CS.GameData.listMallGood.Count - 1, 0, -1 do
		if CS.GameData.listMallGood[i].type == CS.GoodType.payToPassOrder then
			print("one");
			CS.GameData.listMallGood:RemoveAt(i);
		end
	end
	self:Start();
end

if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
	util.hotfix_ex(CS.PassBuyPassBoxController,'RefreshPriceLabel',myRefreshPriceLabel)
	util.hotfix_ex(CS.PassBuyPassBoxController,'OnIAPValidateComplete',myOnIAPValidateComplete)
	util.hotfix_ex(CS.PassBuyPassBoxController,'Start',myStart)
end

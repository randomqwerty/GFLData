local util = require 'xlua.util'
xlua.private_accessible(CS.OneClickBuyPackage)
xlua.private_accessible(CS.ItemPackage)
xlua.private_accessible(CS.QuickPurchaseBox)
local myBuyItemsHandle = function(self)
	--print('myBuyItemsHandle1');
	if(CS.System.Convert.ToInt32(self.oneClickGood.currentGoodType) == 1 and self.oneClickGood.listItemPackage[0].info.itemId ~= 7) then
		self.oneClickGood.mallGoodLeft.requestBuyGoodHandle = function(succeed) self:RequestBuyGoodHandle(succeed); end;
		--if (self.oneClickGood.mallGoodRight ~= nil) then
            self.oneClickGood.mallGoodRight.requestBuyGoodHandle = function(succeed) self:RequestBuyGoodHandle(succeed); end;
		--end
		
        if self.isBuyingDefault then  
			--print('myBuyItemsHandle3');
            self.oneClickGood.mallGoodLeft.buyNum = self.currentNum;
            if (self:MessageGemNotEnough(self.oneClickGood.mallGoodLeft.gemPrice * self.oneClickGood.mallGoodLeft.buyNum)) then
				--print('myBuyItemsHandle4');
                return;
			end
            self.oneClickGood.mallGoodLeft:RequestBuy();
		else
			self.oneClickGood.mallGoodRight.buyNum = self.currentNum;
            if (self:MessageGemNotEnough(self.oneClickGood.mallGoodRight.gemPrice * self.oneClickGood.mallGoodRight.buyNum)) then
                return;
			end
            self.oneClickGood.mallGoodRight:RequestBuy();
		end
	else
		--print('myBuyItemsHandle5');
		self:BuyItemsHandle();
	end
end
local myOneClickBuyItemView = function(self)
	--print('myOneClickBuyItemView');
	self.transform:Find("Frame/Top/Tabs/Tab2").gameObject:SetActive(self.oneClickGood.mallGoodRight ~= self.oneClickGood.mallGoodLeft);
	self:OneClickBuyItemView();
end
local myOneClickBuyPackage = function(self, ...)
	--print('myOneClickBuyPackage1');
	local length = select('#', ...);
    if length == 5 then
		--print('myOneClickBuyPackage2');
		local goodType = select(1, ...);
		local id = select(2, ...);
		local amount = select(3, ...);
		local minGoodAmount = select(4, ...);
		local maxGoodAmount = select(5, ...);
		if(CS.System.Convert.ToInt32(goodType) == 1 and id ~= 7 and self.mallGoodRight == nil) then
			--print('myOneClickBuyPackage3');
			local mallGoodLeft = CS.Data.GetMallGoodInfo(goodType, id, minGoodAmount);
			local itemPackage = CS.ItemPackage(id, amount)
			itemPackage.discount = 1;
            local leftMallBuyAmount = 0;
			if mallGoodLeft.restNumber > amount or mallGoodLeft.restNumber < 0 then
				--print('myOneClickBuyPackage4');
				leftMallBuyAmount = amount;
			else
				--print('myOneClickBuyPackage5');
				if(mallGoodLeft.restNumber > 0) then
					--print('myOneClickBuyPackage6');
					leftMallBuyAmount = mallGoodLeft.restNumber ;
				else
					--print('myOneClickBuyPackage7');
					leftMallBuyAmount = 1;
				end
			end
            itemPackage.leftMallBuyAmount = leftMallBuyAmount;
			itemPackage.rightMallBuyAmount = 1;
			self.listItemPackage:Add(itemPackage);
			self.mallGoodRight = mallGoodLeft;
		end
	end
end
local myInit = function(self, message, data, buyHandler, cancelHandler)
	--print('myOneClickBuyItemView');
	self.transform:Find("Frame/Top/Tabs/Recommended/Tex_Recommended"):GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(1554);;
	self:Init(message, data, buyHandler, cancelHandler);
end
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
util.hotfix_ex(CS.OneClickBuyPackage, '.ctor', myOneClickBuyPackage)
util.hotfix_ex(CS.QuickPurchaseBox, 'BuyItemsHandle', myBuyItemsHandle)
util.hotfix_ex(CS.QuickPurchaseBox, 'Init', myInit)
util.hotfix_ex(CS.QuickPurchaseBox, 'OneClickBuyItemView', myOneClickBuyItemView)
end
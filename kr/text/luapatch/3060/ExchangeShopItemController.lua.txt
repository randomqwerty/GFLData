local util = require 'xlua.util'
xlua.private_accessible(CS.ExchangeShopItemController)
local mallIds = { 310, 313, 314, 315, 316, 317, 318, 319, 320, 321, 322 }

local SetItemDescription = function(self)
	self:SetItemDescription()
	
	if self.currentMallGood.type == 2 and self.currentMallGood.package.listItemPackage.Count > 0 
		and self.currentMallGood.package.listItemPackage[0].info.itemId == 51 then
		self.timeLeft.gameObject:SetActive(false);
	end
end

local Init = function(self,mallGood)
	self:Init(mallGood)
	local meet = false
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Normal and mallGood.type == 2 then
		for i=1,#mallIds do
			if mallGood.id == mallIds[i] then
				meet = true
				break
			end
		end
	end
	if meet and mallGood.package.listItemPackage.Count > 0 then
		local own = CS.GameData.GetItem(mallGood.package.listItemPackage.itemInfoid)
		-- print("explore find mall", mallGood.id, own)
		if own > 0 then
			self:SetSoldOut()
		end
		self.timeLeft.gameObject:SetActive(false)
		self.btnTip.gameObject:SetActive(false)
	end
end

util.hotfix_ex(CS.ExchangeShopItemController,'SetItemDescription',SetItemDescription)
util.hotfix_ex(CS.ExchangeShopItemController,'Init',Init)



local util = require 'xlua.util'
xlua.private_accessible(CS.MallGoodController)

 
local _Start = function(self)
	self:Start();  
	if not self.gameObject.name:find("SkinDisplay") then
		if self.good.type == CS.GoodType.gemToSeven3 or self.good.type == CS.GoodType.gemToSupply or self.good.type == CS.GoodType.gemToGiftbag then
			self:SetQoutaDescription();
			if self.good.restNumber == 0 then
	 			self:SetSoldOut();
			end
		elseif self.good.type == CS.GoodType.payToFirst or self.good.type == CS.GoodType.payToGiftbagCanRest or self.good.type == CS.GoodType.payToGiftbag  then	
			self:SetQoutaDescription();
			if self.good.restNumber == 0 then
	 			self:SetSoldOut();
			end
			self.imgPriceIcon.gameObject:SetActive(false);
		else 
			if self.good.type == CS.GoodType.payToMonthly or self.good.type == CS.GoodType.payToGem then
				self.imgPriceIcon.gameObject:SetActive(false);
				self:UpdateMonthlyCardRestTime();--月卡剩余时间
			end
			if self.good.restNumber > -1 then
				self.imageRemainLabel.gameObject:SetActive(true);
				if self.good.restNumber == 0 then
 				self:SetSoldOut();
				end
			end
		end
	end
	
end 
util.hotfix_ex(CS.MallGoodController,'Start',_Start)



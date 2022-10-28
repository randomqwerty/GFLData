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
local myOnClick = function(self)
	if self.good ~= nil and (self.good.rmbId == "60101" or self.good.rmbId == "60102" or self.good.rmbId == "60103"
			or self.good.rmbId == "60104" or self.good.rmbId == "60105" or self.good.rmbId == "60106" 
			or self.good.rmbId == "60107" or self.good.rmbId == "60112" or self.good.rmbId == "60151") then
		CS.CommonController.LightMessageTips("この商品は現在購入できません。");
	else
		self:OnClick();  
	end
end
local _UpdateGoodUI = function(self,mallGood,pointMall,goodName,description,spriteIcon,count)
	self:UpdateGoodUI(mallGood,pointMall,goodName,description,spriteIcon,count);

	if spriteIcon ~=nil then

	elseif CS.System.String.IsNullOrEmpty(mallGood.icon)==false then

	else 
		local package ;
		if pointMall~= nil then
				package= pointMall.packag;
		else
				package= mallGood.package;
		end
		if package ~= nil then
			if package.listItemPackage.Count > 0 then
				local itemInfo = package.listItemPackage[0].info;
				if itemInfo ~= nil and itemInfo.type == 5 then
					local fc = CS.GameData.listCosmeticMall:GetDataById(itemInfo.itemId - 1000);
					if fc ~= nil then
						if fc.type == CS.CosmeticType.headPic then
							CS.CommonController.LoadImageAvatarWithSequenceFrame(self.imageIcon, fc.id);
						end
						if fc.type == CS.CosmeticType.headFrame then
							CS.CommonController.LoadImageHeadFrameWithSequenceFrame(self.imageIcon, fc.id);
						end
					end
				end
			end
		end
		package=nil;
	end	
end
util.hotfix_ex(CS.MallGoodController,'Start',_Start)
util.hotfix_ex(CS.MallGoodController,'UpdateGoodUI',_UpdateGoodUI)
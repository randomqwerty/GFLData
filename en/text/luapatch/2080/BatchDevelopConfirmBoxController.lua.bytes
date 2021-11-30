local util = require 'xlua.util'
xlua.private_accessible(CS.BatchDevelopConfirmBoxController)
xlua.private_accessible(CS.StatisticsController)
xlua.private_accessible(CS.DevelopEquipmentController)
xlua.private_accessible(CS.FactoryResourceController)
xlua.private_accessible(CS.DevelopController)
xlua.private_accessible(CS.CommonTopController)
local myOnClickItem = function(self, item, isAutoBack)
	if item == nil then

	else
		self:OnClickItem(item, isAutoBack);
	end
end
--local myEquipOnClickItem = function(self, item)
	--print("装备点击");
	--if item == nil then
		--print("item null");
	--else
		--print("item not null");
		--self:OnClickItem(item);
	--end
--end
local myOnClickItemNull = function(self, item, isAutoBack)
	
end
local myRequestStartDevelopEquipHandle = function(self, request)
		xlua.hotfix(CS.DevelopController,"OnClickItem",myOnClickItemNull)
		self:RequestStartDevelopEquipHandle(request);
		util.hotfix_ex(CS.DevelopController,"OnClickItem",myOnClickItem)
        --if request.isQuick == 1 then
			--CS.FactoryResourceController.Close();
            --CS.DevelopEquipmentController.Instance:OnClickItem(CS.DevelopEquipmentController.Instance.currentSelectedItem);
        --end
end
local myRequestStartEquipProduceDevelopHandle = function(self, req)
		xlua.hotfix(CS.DevelopController,"OnClickItem",myOnClickItemNull)
		self:RequestStartEquipProduceDevelopHandle(req);
		util.hotfix_ex(CS.DevelopController,"OnClickItem",myOnClickItem)
		--if req.isQuick == 1 then
			--CS.FactoryResourceController.Close();
            --CS.DevelopEquipmentController.Instance:OnClickItem(CS.DevelopEquipmentController.Instance.currentSelectedItem);
        --end
end
local myRequestWishGunDevelHandle = function(self, request)
	if request.ifQuick == 1 then
		self.gameObject:SetActive(false);
		CS.DevelopController.Instance:UpdateSlots();
		CS.CommonTopController.TriggerRefershResourceEvent();	
		CS.FactoryResourceController.Close();
		CS.DevelopController.Instance:OnClickItem(CS.DevelopController.Instance.currentSelectedItem, true);
	else
		self:RequestWishGunDevelHandle(request);
	end
end
local myInitWish = function(self, type, isWish, gunType)
	if isWish == true and type == CS.DevelopType.SpecialGun then
		if self.ResourceNumber.Count == 6 then
			self.ResourceNumber[4] = CS.Data.GetSpecialDevInputValue(true)[0].core;
			self.ResourceNumber[5] = CS.Data.GetSpecialDevInputValue(true)[0].contract;
			self.OldResourceNumber[4] = self.ResourceNumber[4];
			self.OldResourceNumber[5] = self.ResourceNumber[5];
		end
	end
	self:InitWish(type, isWish, gunType);
	if isWish == true and type == CS.DevelopType.SpecialGun then
		self.textWishGunTipsSp.text = self.textWishGunTips.text;
	end
end
util.hotfix_ex(CS.DevelopController,'OnClickItem',myOnClickItem)
--util.hotfix_ex(CS.DevelopEquipmentController,'OnClickItem',myEquipOnClickItem)
util.hotfix_ex(CS.BatchDevelopConfirmBoxController,'InitWish',myInitWish)
util.hotfix_ex(CS.BatchDevelopConfirmBoxController,'RequestWishGunDevelHandle',myRequestWishGunDevelHandle)
util.hotfix_ex(CS.BatchDevelopConfirmBoxController,'RequestStartDevelopEquipHandle',myRequestStartDevelopEquipHandle)
util.hotfix_ex(CS.BatchDevelopConfirmBoxController,'RequestStartEquipProduceDevelopHandle',myRequestStartEquipProduceDevelopHandle)
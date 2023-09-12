local util = require 'xlua.util'
xlua.private_accessible(CS.PlayerReturnEventCtrl)
xlua.private_accessible(CS.PlayerReturnFundCtrl)
xlua.private_accessible(CS.PassBuyPassBoxController)
xlua.private_accessible(CS.Data)
local Awake = function(self)
	self:Awake();
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
		local imageTrans1 = self.transform:Find("FundsContent/ActivateCard/Img_Bg");
		if imageTrans1~= nil then
			local obj1 = CS.ResManager.GetObjectByPath("AtlasClips3010/回归基金");
			imageTrans1:GetComponent(typeof(CS.ExImage)).sprite = obj1:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite;
		end
	end
end
local _OnIAPValidateComplete = function(self)
	self:OnIAPValidateComplete();

	local Tex_Money = self.transform:Find("ActivateCard/Img_Bg/Tex_Money");
	local Tex_Count = self.transform:Find("ActivateCard/Img_Bg/Tex_Count");
	if self.fundGood ~= nil then
		Tex_Money:GetComponent(typeof(CS.ExText)).text = "";


		local normalPrice = "";
		if (CS.System.String.IsNullOrEmpty(self.fundGood.displayPrice)) then
			normalPrice = CS.Data.GetLang(71011) .. self.fundGood.pointPrice;
		else
			normalPrice = self.fundGood.displayPrice;
		end
		Tex_Count:GetComponent(typeof(CS.ExText)).text = normalPrice;
		self.buyPrice_Tex.text = normalPrice;
	else
		Tex_Money:GetComponent(typeof(CS.ExText)).text = "";
		Tex_Count:GetComponent(typeof(CS.ExText)).text = "";
	end
end
local _PassIAPComplete = function(self)
	self:OnIAPValidateComplete();
	if CS.PassOrderUserData.Instance.normalGood ~= nil then
		self:RefreshPriceLabel();
	end
end
-- local _InitUIElements = function(self)
-- 	print("_InitUIElements");
-- 	xlua.hotfix(CS.Data,'GetPayToGiftbagBuyCount',_GetRestNum)
-- 	self:InitUIElements()
-- end
-- local _CloseView = function(self)
-- 	print("_CloseView");
-- 	xlua.hotfix(CS.Data,'GetPayToGiftbagBuyCount',nil)
-- 	self:CloseView()
-- end
local _GetRestNum = function(good)
	local num=CS.Data.GetPayToGiftbagBuyCount(good);
	
	if good.type == CS.GoodType.payToReturnGiftbag then
		--print("_GetRestNum:"..good.rmbId.."__"..num);
		if num ==0 then
			return 0;
		else
			local qoutaData=nil;
			for l=0,CS.MallGoodResController.listPointMallQouta.Count-1 do
				local dd = CS.MallGoodResController.listPointMallQouta[l];
				if dd.productId == good.rmbId then
					qoutaData=dd;				 
				end				
			end
			if qoutaData~=nil and qoutaData.lastBuyTime >= CS.GameData.userReturnEventData.start_time and qoutaData.lastBuyTime< CS.GameData.userReturnEventData.end_time then
				return qoutaData.buyCount;
			else
				return 0;
			end
		end
	else
		return num
	end
end

--util.hotfix_ex(CS.PlayerReturnEventCtrl,'InitUIElements',_InitUIElements)
--util.hotfix_ex(CS.PlayerReturnEventCtrl,'CloseView',_CloseView)
util.hotfix_ex(CS.Data,'GetPayToGiftbagBuyCount',_GetRestNum)
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
 util.hotfix_ex(CS.PlayerReturnFundCtrl,'OnIAPValidateComplete',_OnIAPValidateComplete)
 util.hotfix_ex(CS.PassBuyPassBoxController,'OnIAPValidateComplete',_PassIAPComplete)
end
--util.hotfix_ex(CS.PlayerReturnEventCtrl,'Awake',Awake)

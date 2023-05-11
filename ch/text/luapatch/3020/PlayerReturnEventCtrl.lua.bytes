local util = require 'xlua.util'
xlua.private_accessible(CS.PlayerReturnEventCtrl)
xlua.private_accessible(CS.PlayerReturnFundCtrl)
xlua.private_accessible(CS.PassBuyPassBoxController)

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
if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Tw or CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_Korea then
 util.hotfix_ex(CS.PlayerReturnFundCtrl,'OnIAPValidateComplete',_OnIAPValidateComplete)
 util.hotfix_ex(CS.PassBuyPassBoxController,'OnIAPValidateComplete',_PassIAPComplete)
end
--util.hotfix_ex(CS.PlayerReturnEventCtrl,'Awake',Awake)

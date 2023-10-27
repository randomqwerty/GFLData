local util = require 'xlua.util'
xlua.private_accessible(CS.MallSkinDisplayController)

local _ShowDeaultItem = function(self,...)
	if self.btnBuy.onClick ~= nil then
		self.btnBuy.onClick:RemoveAllListeners()
	end

	self.btnBuy:AddOnClick(function()
			self:OnBuyClicked()	
			end);
	self:ShowDeaultItem(...);
end

local _InitUIElements = function(self,...)
	self:InitUIElements(...);

	if self.btnBuy.onClick ~= nil then
		self.btnBuy.onClick:RemoveAllListeners()
	end

	self.btnBuy:AddOnClick(function()
			self:OnBuyClicked()	
			end);
end

local _CheckSkinHaveGun = function(self,mallGood)
	local showPurchasePrompt = false;
	local gunId = 0;
	local skinId = 0;
	local skinClassTheme = 0;
	local ret0 = false;
	ret0,gunId,skinId,skinClassTheme = CS.Data.GetMallGoodSkinInfo(mallGood, gunId, skinId, skinClassTheme);
	local tt = (CS.GameData.listGun:Exists((function(g) return g.info.id == gunId or (g.info.isMindupdate and gunId == g.info.gunInfoOtherMod.id); end)));
	showPurchasePrompt = tt == false;
	self.objPurchasePrompt:SetActive(showPurchasePrompt);
end

util.hotfix_ex(CS.MallSkinDisplayController,'ShowDeaultItem',_ShowDeaultItem)
util.hotfix_ex(CS.MallSkinDisplayController,'InitUIElements',_InitUIElements)
util.hotfix_ex(CS.MallSkinDisplayController,'CheckSkinHaveGun',_CheckSkinHaveGun)


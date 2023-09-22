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

util.hotfix_ex(CS.MallSkinDisplayController,'ShowDeaultItem',_ShowDeaultItem)
util.hotfix_ex(CS.MallSkinDisplayController,'InitUIElements',_InitUIElements)


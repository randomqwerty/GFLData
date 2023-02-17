local util = require 'xlua.util'
xlua.private_accessible(CS.FactoryFormulaPreviewTypeHolder)
xlua.private_accessible(CS.CommonIconController)
local _IconInit = function(self)
	local txt1 = self.transform:Find("HaveDropGun/Image/UI_Text"):GetComponent(typeof(CS.ExText));
	if txt1~=nil then 
		txt1.text = CS.Data.GetLang(30494);
	end 
end
local _InitUIElements = function(self)
	self:InitUIElements(); 
	xlua.hotfix(CS.CommonIconController,'Awake',_IconInit)
end
local _OnDestroy = function(self)
	xlua.hotfix(CS.CommonIconController,'Awake',nil)
	self:OnDestroy();
end
util.hotfix_ex(CS.FactoryFormulaPreviewTypeHolder,'InitUIElements',_InitUIElements)
util.hotfix_ex(CS.FactoryFormulaPreviewTypeHolder,'OnDestroy',_OnDestroy)



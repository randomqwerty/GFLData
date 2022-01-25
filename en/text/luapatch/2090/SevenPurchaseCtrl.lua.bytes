local util = require 'xlua.util'
xlua.private_accessible(CS.SevenPurchaseCtrl)

local InitUIElements= function(self)
	self:InitUIElements();
	local topTime = self.transform:Find("Left/Title/Img_Title");
	local obj1 = CS.ResManager.GetObjectByPath("AtlasClips2090/未标题-1_07");
	if obj1 ~= nil then
		topTime:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite = obj1:GetComponent(typeof(CS.UnityEngine.UI.Image)).sprite;
	end
end

util.hotfix_ex(CS.SevenPurchaseCtrl,'InitUIElements',InitUIElements)

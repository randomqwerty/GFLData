local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentUIController)

local LoadItemData = function(self)
	self:LoadItemData();
	if self.itemObj ~= nil and not self.itemObj:isNull() then
		local rectTrans = self.itemObj:GetComponent(typeof(CS.UnityEngine.RectTransform));
		rectTrans.anchorMin = CS.UnityEngine.Vector2.one;
		rectTrans.anchorMax = CS.UnityEngine.Vector2.one;
		if self:canShowFightBuffUI() then
			rectTrans.anchoredPosition = CS.UnityEngine.Vector2(270,-330);
		else
			rectTrans.anchoredPosition = CS.UnityEngine.Vector2(270,-70);
		end
	end
end
local ItemObjMoveLeft = function(self)
	if self.itemObj ~= nil and not self.itemObj:isNull() then
		local rectTrans = self.itemObj:GetComponent(typeof(CS.UnityEngine.RectTransform));
		rectTrans:DOAnchorPosX(70,0.5):SetEase(CS.DG.Tweening.Ease.OutBack);
	end
end
local ItemObjMoveReast = function(self)
	if self.itemObj ~= nil and not self.itemObj:isNull() then
		local rectTrans = self.itemObj:GetComponent(typeof(CS.UnityEngine.RectTransform));
		rectTrans:DOAnchorPosX(270,0.5):SetEase(CS.DG.Tweening.Ease.OutBack);
	end
end
util.hotfix_ex(CS.DeploymentUIController,'LoadItemData',LoadItemData)
util.hotfix_ex(CS.DeploymentUIController,'ItemObjMoveLeft',ItemObjMoveLeft)
util.hotfix_ex(CS.DeploymentUIController,'ItemObjMoveReast',ItemObjMoveReast)

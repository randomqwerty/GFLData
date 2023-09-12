local util = require 'xlua.util'
xlua.private_accessible(CS.BattleUIController)

local Start = function(self)
	self:Start();
	local panelUI = self.TranAutoBattle:GetComponent(typeof(CS.UnityEngine.RectTransform));
	panelUI.anchorMax = CS.UnityEngine.Vector2.one;
	panelUI.anchorMin = CS.UnityEngine.Vector2.zero;
	panelUI.offsetMin = CS.UnityEngine.Vector2(0,-384);
	panelUI.offsetMax = CS.UnityEngine.Vector2.zero;
	local bg = self.TranAutoBattle:Find("Img_Bg"):GetComponent(typeof(CS.UnityEngine.RectTransform));
	bg.anchorMin = CS.UnityEngine.Vector2(0,1);
	bg.anchorMax = CS.UnityEngine.Vector2.one;
	bg.anchoredPosition = CS.UnityEngine.Vector2(bg.anchoredPosition.x,-143);
	bg.sizeDelta = CS.UnityEngine.Vector2(bg.sizeDelta.x,286);
end

util.hotfix_ex(CS.BattleUIController,'Start',Start)
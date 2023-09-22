local util = require 'xlua.util'
xlua.private_accessible(CS.DailyExploreUIController)

local Awake = function(self)
	self:Awake();
	local rectTransform = self.btnAutoPlan.targetGraphic.rectTransform;
	rectTransform.anchorMin = CS.UnityEngine.Vector2(0,0);
	rectTransform.anchorMax = CS.UnityEngine.Vector2(0,0);
	rectTransform.pivot = CS.UnityEngine.Vector2(0.5,0.5);
	rectTransform.anchoredPosition = CS.UnityEngine.Vector2(115,375);
	local tweenplay = self.btnAutoPlan:GetComponent(typeof(CS.TweenPlay));
	tweenplay.fromThree = CS.UnityEngine.Vector3(115,425,0);
	tweenplay.toThree = CS.UnityEngine.Vector3(115,375,0);
	local res = self.transform:Find("PlanMode/Res"):GetComponent(typeof(CS.UnityEngine.RectTransform));
	res.anchorMin = CS.UnityEngine.Vector2(1,1);
	res.anchorMax = CS.UnityEngine.Vector2(1,1);
	res.pivot = CS.UnityEngine.Vector2(0.5,0.5);
	res.anchoredPosition = CS.UnityEngine.Vector2(-340,-87);
end

util.hotfix_ex(CS.DailyExploreUIController,'Awake',Awake)


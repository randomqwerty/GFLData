local util = require 'xlua.util'
xlua.private_accessible(CS.MotherBaseController)

local Awake = function(self)
	self:Awake();
	local rectTransform = self.btnReturn.targetGraphic.rectTransform;
	rectTransform.anchorMin = CS.UnityEngine.Vector2(0,1);
	rectTransform.anchorMax = CS.UnityEngine.Vector2(0,1);
	rectTransform.pivot = CS.UnityEngine.Vector2(0,1);
	rectTransform.anchoredPosition = CS.UnityEngine.Vector2(0,0);
end

util.hotfix_ex(CS.MotherBaseController,'Awake',Awake)


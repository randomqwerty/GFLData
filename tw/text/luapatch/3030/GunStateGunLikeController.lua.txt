local util = require 'xlua.util'
xlua.private_accessible(CS.GunStateGunLikeController)

local Start = function(self)
	self:Start();
	local rectTransform = self.rectTransform;
	rectTransform.anchorMin = CS.UnityEngine.Vector2(0.5,0.5);
	rectTransform.anchorMax = CS.UnityEngine.Vector2(0.5,0.5);
	rectTransform.anchoredPosition = CS.UnityEngine.Vector2(817,-473);
end

util.hotfix_ex(CS.GunStateGunLikeController,'Start',Start)
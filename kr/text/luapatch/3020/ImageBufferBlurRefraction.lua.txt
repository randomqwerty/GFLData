local util = require 'xlua.util'
xlua.private_accessible(CS.ImageBufferBlurRefraction)

local Awake = function(self)
	self:Awake();
	local scale = CS.ImageBufferBlurRefraction.MessageboxCanvas.gameObject:GetComponent(typeof(CS.UnityEngine.UI.CanvasScaler));
	if CS.Utility.rr >1.01 then
		scale.referenceResolution = CS.UnityEngine.Vector2(CS.Utility.rr*2048,1536);
	end
end
util.hotfix_ex(CS.ImageBufferBlurRefraction,'Awake',Awake)
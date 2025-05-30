local util = require 'xlua.util'
xlua.private_accessible(CS.CommonLive2DController)


local SetScenePosNew = function(self)
	self:SetScenePosNew();
	self.pos = self.gameObject:GetComponent(typeof(CS.UnityEngine.RectTransform)).anchoredPosition;
end

util.hotfix_ex(CS.CommonLive2DController,'SetScenePosNew',SetScenePosNew)

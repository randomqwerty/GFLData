local util = require 'xlua.util'
xlua.private_accessible(CS.CommonVideoPlayer)

local Start = function(self)
	self:Start();
	if CS.OPSPanelController.Instance ~= nil and not CS.OPSPanelController.Instance:isNull() then
		if CS.OPSPanelController.Instance.campaionId == -68 then
			print("修改比例");
			self.canvasScaler.referenceResolution = CS.UnityEngine.Vector2(2048,1536);
			self.imgVideo:GetComponent(typeof(CS.UnityEngine.RectTransform)).sizeDelta = CS.UnityEngine.Vector2(2048,1536);
			self.imgVideo.rectTransform.sizeDelta = CS.UnityEngine.Vector2(2048,1536);
		end
	end
end

util.hotfix_ex(CS.CommonVideoPlayer,'Start',Start)


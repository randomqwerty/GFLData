local util = require 'xlua.util'
xlua.private_accessible(CS.CommonVideoPlayer)

local Start = function(self)
	self:Start();
	if CS.OPSPanelController.Instance ~= nil and not CS.OPSPanelController.Instance:isNull() then
		if CS.OPSPanelController.Instance.campaionId == -68 then
			if CS.Data.GetPlayerPrefStringsExists("CampaionVideo","-68") then
				print("修改MatchWidthOrHeight");
				self:SetAsMatchWidthCanvas();
				self.canvasScaler.referenceResolution = CS.UnityEngine.Vector2(2048,1536);
				self.imgVideo.rectTransform.sizeDelta = CS.UnityEngine.Vector2(2048,1536);
			else
				print("修改Expand");
				self:SetAsExpandCanvas();
				self.canvasScaler.referenceResolution = CS.UnityEngine.Vector2(2048,1152);
				self.imgVideo.rectTransform.sizeDelta = CS.UnityEngine.Vector2(2048,1152);
			end
		end
	end
end

local RestartVideo = function(self)
	self:RestartVideo();
	if CS.OPSPanelController.Instance ~= nil and not CS.OPSPanelController.Instance:isNull() then
		if CS.OPSPanelController.Instance.campaionId == -68 then
			print("修改MatchWidthOrHeight");
			self:SetAsMatchWidthCanvas();
			self.canvasScaler.referenceResolution = CS.UnityEngine.Vector2(2048,1536);
			self.imgVideo.rectTransform.sizeDelta = CS.UnityEngine.Vector2(2048,1536);
		end
	end
end
util.hotfix_ex(CS.CommonVideoPlayer,'Start',Start)
util.hotfix_ex(CS.CommonVideoPlayer,'RestartVideo',RestartVideo)


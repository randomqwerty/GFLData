local util = require 'xlua.util'
xlua.private_accessible(CS.IllustratedBookAchievementItemController)

local mInit = function(self,info,showMoreBtn)
	self:Init(info,showMoreBtn)
	self.scrollSequence = -1;
	self.textRewardExtra.rectTransform:DOKill();
	self.textRewardExtra.rectTransform.pivot = CS.UnityEngine.Vector2(0,0.5)
	
	local content_size=self.textRewardExtra.gameObject:GetComponent(typeof(CS.UnityEngine.UI.ContentSizeFitter))
	if content_size==nil then
		content_size=self.textRewardExtra.gameObject:AddComponent(typeof(CS.UnityEngine.UI.ContentSizeFitter))
	end
	if content_size~=nil then
		content_size.horizontalFit=CS.UnityEngine.UI.ContentSizeFitter.FitMode.PreferredSize
	end
	local parent = self.textRewardExtra.transform.parent
	local rollingText=parent.gameObject:GetComponent(typeof(CS.RollingText))
	if rollingText==nil then
		rollingText=parent.gameObject:AddComponent(typeof(CS.RollingText))
	end
	if rollingText~=nil then
		--rollingText:SetText(info.package:ToString(false, true))
		rollingText:SetText(self.textRewardExtra.text)
	end
end
util.hotfix_ex(CS.IllustratedBookAchievementItemController,'Init',mInit)
local util = require 'xlua.util'
xlua.private_accessible(CS.GuideManagerController)

local CheckHand = function(self)
	self.animatorLittleHand.enabled = false;
	self.animatorLittleHand.transform:GetChild(0).localPosition = CS.UnityEngine.Vector3.zero;
	self.animatorLittleHand.enabled = true;
	self:CheckHand();
end
util.hotfix_ex(CS.GuideManagerController,'CheckHand',CheckHand)

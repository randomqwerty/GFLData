local util = require 'xlua.util'
xlua.private_accessible(CS.RewardBoxController)

local mOnClickClose = function(self)
	if CS.SangvisCaptureController.Instance~=nil and CS.CommonSceneManagerController.instance.currentSceneName == "SangvisGasha" then
		CS.SangvisCaptureController.Instance.graphicRaycaster.enabled = true;
		
	end
	self:OnClickClose();
end
util.hotfix_ex(CS.RewardBoxController,'OnClickClose',mOnClickClose)


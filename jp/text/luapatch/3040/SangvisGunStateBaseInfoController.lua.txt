local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisGunStateBaseInfoController)

local mJumpToTransfer = function(self)
	if CS.CommonSceneManagerController.instance.currentSceneName == "Theater" then
		CS.CommonController.LightMessageTips(CS.Data.GetLang(1757));	
	else
		self:JumpToTransfer();
	end
end

local mOnClickAdvance = function(self)
	if CS.CommonSceneManagerController.instance.currentSceneName == "Theater" then
		CS.CommonController.LightMessageTips(CS.Data.GetLang(1757));
	else
		self:OnClickAdvance();
	end
end
util.hotfix_ex(CS.SangvisGunStateBaseInfoController,'JumpToTransfer',mJumpToTransfer)
util.hotfix_ex(CS.SangvisGunStateBaseInfoController,'OnClickAdvance',mOnClickAdvance)
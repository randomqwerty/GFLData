local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisGunStateBaseInfoController)

local mJumpToTransfer = function(self)
	if CS.CommonSceneManagerController.instance.currentSceneName == "Formation" then
			if CS.CommonSangvisCharacterListController.Instance ~=nil then
				CS.CommonSangvisCharacterListController.Instance:Hide();
			end	
	end
	self:JumpToTransfer();
end


util.hotfix_ex(CS.SangvisGunStateBaseInfoController,'JumpToTransfer',mJumpToTransfer)

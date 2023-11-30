local util = require 'xlua.util'
xlua.private_accessible(CS.QuickJumpBtnController)

local mSwitchNavigationController = function(self)

	if CS.CommonSceneManagerController.instance.currentSceneName == "Formation" and CS.FormationController.Instance ~= nil then
		local san = CS.Data.EverySangvisTeamIsAvailable();
		--print(san)
		if san~= -1 then
			CS.FormationController.Instance:OnClickCheckIsAllOfTeamExistLeader();
		else 
			self:SwitchNavigationController();
		end
	else
		self:SwitchNavigationController();
	end
end

util.hotfix_ex(CS.QuickJumpBtnController,'SwitchNavigationController',mSwitchNavigationController)
local util = require 'xlua.util'
xlua.private_accessible(CS.BattleUIDefenseTrialResultController)
xlua.private_accessible(CS.CommonSceneManagerController)
local myOnClick = function(self)
	if self.canSkip then
		if CS.CommonSceneManagerController.instance.currentSceneName == "Battle" then
			CS.CommonSceneManagerController.instance:Clear();
		end
	end 
	self:OnClick();
end
util.hotfix_ex(CS.BattleUIDefenseTrialResultController,'OnClick',myOnClick)
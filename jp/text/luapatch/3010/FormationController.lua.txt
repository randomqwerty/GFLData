local util = require 'xlua.util'
xlua.private_accessible(CS.FormationController)
xlua.private_accessible(CS.SquadStateController)
local myShowUI = function(self)
    self:ShowUI()
	if(CS.SquadStateController.Instance ~= nil and CS.SquadStateController.Instance.gameObject.activeInHierarchy) then
		CS.SquadStateController.Instance.transform:SwitchSidebar("", true);
	end
end
util.hotfix_ex(CS.FormationController,'ShowUI',myShowUI)
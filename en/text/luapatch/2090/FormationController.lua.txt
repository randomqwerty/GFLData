local util = require 'xlua.util'
xlua.private_accessible(CS.FormationController)
local myStart = function(self)
    self:Start()
	if(CS.FormationController.lastScene == "Battle") then
		CS.QuickJumpBtnController.Instance.gameObject:SetActive(false);
	end		
end
util.hotfix_ex(CS.FormationController,'Start',myStart)
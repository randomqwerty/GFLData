local util = require 'xlua.util'
xlua.private_accessible(CS.AVGCreditsController)
local myStart = function(self)
    self:Start();
	CS.AVGController.Instance.goSkip:SetActive(false);
end

util.hotfix_ex(CS.AVGCreditsController,'Start',myStart)

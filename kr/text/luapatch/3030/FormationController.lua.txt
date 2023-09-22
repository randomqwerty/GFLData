local util = require 'xlua.util'
xlua.private_accessible(CS.FormationController)
local ShowEfficiencyUI = function(self)
	CS.CommonController.mainController = CS.CommonController.MainCanvas.gameObject;
	self:ShowEfficiencyUI();
end
util.hotfix_ex(CS.FormationController,'ShowEfficiencyUI',ShowEfficiencyUI)

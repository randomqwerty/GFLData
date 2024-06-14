local util = require 'xlua.util'
xlua.private_accessible(CS.CommonSquadListLabelController)

local mShowEfficiencyUI = function(self)

	if CS.SquadListController.Instance~=nil and CS.SquadListController.Instance.showType == CS.SquadListType.TargetTrain then
		--print("TargetTrain")
		return;
	else
		self:mShowEfficiencyUI();
	end

end
util.hotfix_ex(CS.CommonSquadListLabelController,'ShowEfficiencyUI',mShowEfficiencyUI)


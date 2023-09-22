local util = require 'xlua.util'
xlua.private_accessible(CS.CommonSquadListLabelController)

local ShowEfficiencyUI = function(self)
	if CS.DeploymentUIController.Instance ~= nil then
		CS.DeploymentEffectivenessController.OpenSquadUI(self.squad, CS.DeploymentUIController.Instance.transform);
	else
		local parent = self.transform.parent;
		if CS.CommonController.mainController ~= nil then
			parent = CS.CommonController.mainController.transform;
		end
		CS.DeploymentEffectivenessController.OpenSquadUI(self.squad, parent);
	end
end

local Awake = function(self)
	self:Awake();
	local list = self.transform:Find("List");
	list:SetAsLastSibling();
end
util.hotfix_ex(CS.CommonSquadListLabelController,'ShowEfficiencyUI',ShowEfficiencyUI)
util.hotfix_ex(CS.CommonSquadListLabelController,'Awake',Awake)

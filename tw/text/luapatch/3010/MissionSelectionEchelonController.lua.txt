local util = require 'xlua.util'
xlua.private_accessible(CS.MissionSelectionEchelonController)


local RequestStartAutoMissionHandler = function(self,result)
	if CS.OPSPanelController.Instance ~= nil then
		CS.CommonTopController.TriggerRefershResourceEvent();
		self:Close();
		if CS.SpecialMissionInfoController.Instance ~= nil then
			CS.SpecialMissionInfoController.Instance:RefresCommonUI();
		end
		return;
	end
	self:RequestStartAutoMissionHandler(result);
end
util.hotfix_ex(CS.MissionSelectionEchelonController,'RequestStartAutoMissionHandler',RequestStartAutoMissionHandler)
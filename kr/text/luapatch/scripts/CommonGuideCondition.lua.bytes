local util = require 'xlua.util'

--指定关卡10
Test1 = function()
	if CS.DeploymentController.Instance == nil then
		return false;
	end
	if CS.GameData.currentSelectedMissionInfo.id == 10 then
		return true;
	end
	return false;
end
--指定type20的building
Test2 = function()
	if CS.DeploymentController.Instance == nil then
		return false;
	end
	for i=0,CS.DeploymentBackgroundController.Instance.listBuildingController.Count-1 do
		local build = CS.DeploymentBackgroundController.Instance.listBuildingController[i];
		if build.buildAction.buildingInfo.type == 20 then
			return true;
		end
	end
	return false;
end


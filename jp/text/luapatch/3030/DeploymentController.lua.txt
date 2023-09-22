local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentController)

local RequestEndAllFriendTurnHandle = function(self,data)
	if data.jsonData:Contains("spot_trans") then
		local json = data.jsonData:GetValue("spot_trans");
		CS.GameData.missionAction:LoadSpotTransData(json);
	end
	self:RequestEndAllFriendTurnHandle(data);
end
local TriggerStartMissionEvent = function()
	if CS.DeploymentAutoBattleController.isDailyMissionInfo(CS.DailyMapHexType.Squad) then
		if CS.DeploymentController.Instance.SquadTeamsCount == 0 then
			CS.CommonController.MessageBox(CS.Data.GetLang(30556));
			return;
		end
	elseif CS.DeploymentAutoBattleController.isDailyMissionInfo(CS.DailyMapHexType.Vehicle) then
		if CS.DeploymentController.Instance.VehicleTeamCount == 0 then
			CS.CommonController.MessageBox(CS.Data.GetLang(30556));
			return;
		end
	end
	CS.DeploymentController.TriggerStartMissionEvent();
end
util.hotfix_ex(CS.DeploymentController,'RequestEndAllFriendTurnHandle',RequestEndAllFriendTurnHandle)
util.hotfix_ex(CS.DeploymentController,'TriggerStartMissionEvent',TriggerStartMissionEvent)


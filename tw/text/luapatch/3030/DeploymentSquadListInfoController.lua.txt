local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentSquadListInfoController)

local Deploy = function(self)
	if CS.SquadListController.Instance.chooseType == CS.SquadInfoCategory.fireTeam then		
		if self.currentSelectSquad ~= nil and not self.currentSelectSquad:isNull() then
			if	self.showtype == CS.SquadListType.AllyInstead then
				self:SetAllySquad(self.currentSelectSquad.squad);
				self.gameObject:SetActive(false);
				return;
			end
			if CS.GameData.currentSelectedMissionInfo.squadLimitTeam == -1 then
				CS.CommonController.LightMessageTips(CS.Data.GetLang(30384));
				return;
			end
			if CS.GameData.currentSelectedMissionInfo.squadLimitTeam ~= 0 and CS.DeploymentController.Instance.SquadTeamsCount>=CS.GameData.currentSelectedMissionInfo.squadLimitTeam then
				CS.CommonController.LightMessageTips(CS.Data.GetLang(10198));
				return;
			end
			if CS.GameData.currentSelectedMissionInfo.totalTeamLimit > 0 and CS.GameData.currentSelectedMissionInfo.basesquadCanTotalTeam then
				if CS.DeploymentController.Instance.TotalTeamsCount >= CS.GameData.currentSelectedMissionInfo.totalTeamLimit then
					CS.CommonController.LightMessageTips(CS.Data.GetLang(10195));
					return;
				end
			end
			if CS.DeploymentTeamInfoController.Instance:ReinforceSquadTeam(self.currentSelectSquad) then
				self:Close();
			end
		end
	end
	if CS.SquadListController.Instance.chooseType == CS.SquadInfoCategory.carrier then
		if self.currentSelectVehicleLabel ~= nil and not self.currentSelectVehicleLabel:isNull() then
			if	self.showtype == CS.SquadListType.AllyInstead then
				self:SetAllyVehicle(self.currentSelectVehicleLabel.vehicle);
				self.gameObject:SetActive(false);
				return;
			end
			if CS.GameData.currentSelectedMissionInfo.vehicleLimitTeam == -1 then
				CS.CommonController.LightMessageTips(CS.Data.GetLang(30384));
				return;
			end
			if CS.GameData.currentSelectedMissionInfo.vehicleLimitTeam ~= 0 and CS.DeploymentController.Instance.VehicleTeamCount>=CS.GameData.currentSelectedMissionInfo.vehicleLimitTeam then
				CS.CommonController.LightMessageTips(CS.Data.GetLang(10198));
				return;
			end
			if CS.GameData.currentSelectedMissionInfo.totalTeamLimit > 0 and CS.GameData.currentSelectedMissionInfo.basesquadCanTotalTeam then
				if CS.DeploymentController.Instance.TotalTeamsCount >= CS.GameData.currentSelectedMissionInfo.totalTeamLimit then
					CS.CommonController.LightMessageTips(CS.Data.GetLang(10195));
					return;
				end
			end
			if CS.DeploymentTeamInfoController.Instance:ReinforceVehicleTeam(self.currentSelectVehicleLabel) then
				self:Close();
			end
		end	
	end
end

util.hotfix_ex(CS.DeploymentSquadListInfoController,'Deploy',Deploy)
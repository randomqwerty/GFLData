local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentBuildingController)

local CheckSkillDetail = function(self,skill)
	local check = self:CheckSkillDetail(skill);
	local checkSpots = CS.System.Collections.Generic.List(CS.SpotAction)(); 
	for i=0,skill.targetSpotAction.Count-1 do
		local spotAction = skill.targetSpotAction[i];
		if CS.GameData.currentSelectedMissionInfo.specialType == CS.MapSpecialType.Night then
			if not spotAction.spot.Show and spotAction.spot.buildingAction == null then
				checkSpots:Add(spotAction);
			end
		end
	end
	for i=0,checkSpots.Count-1 do
		skill.targetSpotAction:Remove(skill.targetSpotAction[i]);
	end
	return skill.targetSpotAction.Count > 0;
end
local CurrentTeamEchelon = function(self)
	if self.currentTeam ~= nil and not self.Show then
		if self.currentTeam:CurrentTeamBelong() ~= CS.TeamBelong.friendly then
			return 0;
		end
	end
	return self:CurrentTeamEchelon();
end
local ShowSangvisSelectTarget = function(self,order)
	self.selectSpots:Clear();
	self:ShowSangvisSelectTarget(order);

	if self.chipData ~= nil and self.chipData.chipCfg.CurrentSpecialType == CS.SangvisChipCfg.ChipSpecialType.TransportAmo then
		if self.selectSpots.Count == 0 then
			return;
		end
		for i=0,self.selectSpots.Count-1 do
			self.selectSpots[i]:HideSkillTarget();
		end
		self.selectSpots:Clear();
		local spots = self.sangvisTeam.teamController.currentSpot:GetSpotsRange(-1, 1);
		for i=0,spots.Count-1 do
			local spot = spots[i];
			if spot.currentTeam ~= nil and spot.currentTeam:CanPlayerHandControl() and spot.currentTeam:CanSupply() then
				self.selectSpots:Add(spot);
			end
		end
		for i=0,self.selectSpots.Count-1 do
			self.selectSpots[i]:ShowSkillTarget();
		end
		if self.selectSpots.Count == 0 then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(30187));
			self:CloseAllSelectTarget();
		end
	end
end
--util.hotfix_ex(CS.DeploymentBuildingController,'CheckSkillDetail',CheckSkillDetail)
util.hotfix_ex(CS.DeploymentSpotController,'CurrentTeamEchelon',CurrentTeamEchelon)
util.hotfix_ex(CS.DeploymentSangvisSkillPanelController,'ShowSangvisSelectTarget',ShowSangvisSelectTarget)
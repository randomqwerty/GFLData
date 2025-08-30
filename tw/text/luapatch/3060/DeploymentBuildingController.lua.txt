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

local LoadItemData = function(self)
	self:LoadItemData();
	self:ItemObjMoveReast();
end

local SelectCancelSpot = function(self,select)
	self:SelectCancelSpot(select);
	if select then
		self:ShowAllSelectTarget();
	else
		self:CloseAllSelectTarget();
	end
end
--util.hotfix_ex(CS.DeploymentBuildingController,'CheckSkillDetail',CheckSkillDetail)

local CheckTeamMoveCost = function(self,showTip)
	if self.vehicleTeam ~= nil then
		if self:CurrentBuffNeedCostAp() >0 then
			if CS.GameData.missionAction.ap < self:CurrentBuffNeedCostAp() then
				if showTip then
					CS.CommonController.LightMessageTips(CS.Data.GetLang(30506));
				end
				return false;
			end
		end 
	end	
	return self:CheckTeamMoveCost(showTip);
end

local AddAndPlayPlayBattleChange = function(self)
	if CS.GameData.missionResult ~= nil then
		self:AddAndPlayPerformance(nil);
		self:AddAndPlayPerformance(function()
			CS.GameData.missionAction.queuePerformanceHandler:Clear();
			CS.DeploymentController.TriggerFinishMissionEvent();
		end)		
		return;
	end
	self:AddAndPlayPlayBattleChange();
end
local RequestStartMission = function(self)
	CS.DeploymentController.savePlayQueue:Clear();
	self:RequestStartMission();
end
local UpdateInfo = function(self)
	if self.teamId>0 then
		self.simpleSaveNode.gameObject:SetActive(true);
	end
	self:UpdateInfo();
end
local CheckBattle = function(self)
	if self:HasTeamCanTrans() then
		CS.DeploymentController.hasTeamTraning = true;
		self:CheckTeamTrans();
		return;
	end
	CS.DeploymentController.hasTeamTraning = false;
	self:CheckBattle();
end
local TriggerAVGFinishEvent = function()
	local team = nil;
	if CS.DeploymentController.Instance ~= nil and not CS.DeploymentController.Instance:isNull() then
		team = CS.DeploymentController.Instance.currentSelectedTeam;
	end
	CS.DeploymentController.TriggerAVGFinishEvent();
	if CS.DeploymentController.Instance ~= nil and not CS.DeploymentController.Instance:isNull() then
		CS.DeploymentController.Instance:SelectTeam(team,true);
	end
end

local OnClickButton = function(self,Button)
	if CS.CommonConfirmBoxControllerNew.hasOpen then
		return;
	end
	self:OnClickButton(Button);
end
local OnClickTeam = function(self,spot)
	if CS.CommonConfirmBoxControllerNew.hasOpen then
		return;
	end
	self:OnClickTeam(spot);
end
util.hotfix_ex(CS.DeploymentSpotController,'CurrentTeamEchelon',CurrentTeamEchelon)
util.hotfix_ex(CS.DeploymentSangvisSkillPanelController,'ShowSangvisSelectTarget',ShowSangvisSelectTarget)
util.hotfix_ex(CS.DeploymentUIController,'LoadItemData',LoadItemData)
util.hotfix_ex(CS.DeploymentBuildSkillItem,'SelectCancelSpot',SelectCancelSpot)
util.hotfix_ex(CS.DeploymentTeamController,'CheckTeamMoveCost',CheckTeamMoveCost)
util.hotfix_ex(CS.DeploymentController,'AddAndPlayPlayBattleChange',AddAndPlayPlayBattleChange)
util.hotfix_ex(CS.DeploymentController,'RequestStartMission',RequestStartMission)
util.hotfix_ex(CS.DeploymentController,'TriggerAVGFinishEvent',TriggerAVGFinishEvent)
util.hotfix_ex(CS.DeploymentController,'CheckBattle',CheckBattle)
util.hotfix_ex(CS.DeploymentFloatingTeamInfo,'UpdateInfo',UpdateInfo)
util.hotfix_ex(CS.DeploymentUIController,'OnClickButton',OnClickButton)
util.hotfix_ex(CS.DeploymentTeamInfoController,'OnClickTeam',OnClickTeam)
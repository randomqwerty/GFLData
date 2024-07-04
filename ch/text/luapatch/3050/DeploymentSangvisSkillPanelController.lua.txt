local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentSangvisSkillPanelController)

local selectSpots1;
local selectSpots2;
local selectSpots3;

local ShowSangvisSelectTarget = function(self,order)
	if order == 0 or order == 1 then
		self:ShowSangvisSelectTarget(order);
		return;
	end
	self:CloseAllSelectTarget();
	self.chipData = nil;
	self.selectMissionSkillCfg = self.sangvisTeam.leaderMissionSkill;
	if self.selectMissionSkillCfg ~= nil then
		if self.sangvisTeam.skill2cdTurn > CS.GameData.missionAction.turn then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(30391));
			return;
		end
		if not self.canCastSkill3 then
			CS.CommonController.LightMessageTips(self.showTip3);
			return;
		end
	end
	if selectSpots3.Count == 0 then
		CS.CommonController.LightMessageTips(CS.Data.GetLang(30187));
		return;
	end
	self.isInSelectTarget = true;
	local skillTransform = self.skill3Trans; 
	skillTransform:Find("Img_IconBg/ActiveSfx").gameObject:SetActive(true);
	skillTransform:Find("Btn_Release").gameObject:SetActive(false);
	skillTransform:Find("Btn_Cancel").gameObject:SetActive(true);
	self.selectSpots = CS.System.Collections.Generic.List(CS.DeploymentSpotController)(selectSpots3);
	for i=0,self.selectSpots.Count-1 do
		self.selectSpots[i]:ShowSkillTarget();
	end
	CS.DeploymentUIController.Instance:CloseBuildControlUI();
end

local ShowVehicleSelectTarget = function(self,order)
	self:CloseAllSelectTarget();
	local skillTransform = nil;
	print(order);
	if order == 1 then
		skillTransform = self.skill1Trans;
		self.selectMissionSkillCfg = self.vehicleTeam:GetMissionSkill(1);
		if self.vehicleTeam.skill1cdTurn > CS.GameData.missionAction.turn then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(30391));
			return;
		end
		self.selectSpots = CS.System.Collections.Generic.List(CS.DeploymentSpotController)(selectSpots1);
	elseif order == 2 then
		skillTransform = self.skill2Trans;
		self.selectMissionSkillCfg = self.vehicleTeam:GetMissionSkill(2);
		if self.vehicleTeam.skill2cdTurn > CS.GameData.missionAction.turn then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(30391));
			return;
		end
		self.selectSpots = CS.System.Collections.Generic.List(CS.DeploymentSpotController)(selectSpots2);
	elseif order == 3 then
		skillTransform = self.skill3Trans;
		self.selectMissionSkillCfg = self.vehicleTeam:GetMissionSkill(3);
		if self.vehicleTeam.skill3cdTurn > CS.GameData.missionAction.turn then
			CS.CommonController.LightMessageTips(CS.Data.GetLang(30391));
			return;
		end
		self.selectSpots = CS.System.Collections.Generic.List(CS.DeploymentSpotController)(selectSpots3);
	end
	if self.selectMissionSkillCfg ~= nil then
		if order == 1 then
			if not self.canCastSkill1 then
				CS.CommonController.LightMessageTips(self.showTip1);
				return;
			end
		elseif order == 2 then
			if not self.canCastSkill2 then
				CS.CommonController.LightMessageTips(self.showTip2);
				return;
			end
		elseif order == 3 then
			if not self.canCastSkill3 then
				CS.CommonController.LightMessageTips(self.showTip3);
				return;
			end
		end
	end
	self.isInSelectTarget = true;
	skillTransform:Find("Img_IconBg/ActiveSfx").gameObject:SetActive(true);
	skillTransform:Find("Btn_Release").gameObject:SetActive(false);
	skillTransform:Find("Btn_Cancel").gameObject:SetActive(true);
	for i=0,self.selectSpots.Count-1 do
		self.selectSpots[i]:ShowSkillTarget();
	end
	CS.DeploymentUIController.Instance:CloseBuildControlUI();
end

local RefreshVehicleSkill1 = function(self)
	self:RefreshVehicleSkill1();
	selectSpots1 = CS.System.Collections.Generic.List(CS.DeploymentSpotController)(self.selectSpots);
end

local RefreshVehicleSkill2 = function(self)
	self:RefreshVehicleSkill2();
	selectSpots2 = CS.System.Collections.Generic.List(CS.DeploymentSpotController)(self.selectSpots);
end

local RefreshVehicleSkill3 = function(self)
	self:RefreshVehicleSkill3();
	local btn = self.skill3Trans:Find("Btn_Release"):GetComponent(typeof(CS.ExButton));
	btn.onClick:RemoveAllListeners();
	btn:AddOnClick(function()
			CS.DeploymentSangvisSkillPanelController.instance:ShowVehicleSelectTarget(3);
		end)
	selectSpots3 = CS.System.Collections.Generic.List(CS.DeploymentSpotController)(self.selectSpots);
end

local RefreshSangvisSkill3 = function(self)
	self:RefreshSangvisSkill3();
	selectSpots3 = CS.System.Collections.Generic.List(CS.DeploymentSpotController)(self.selectSpots);
end
local CheckMissionSkillCost = function(self,skillTrans,missionSkillCfg,order)
	if self.currentSelectedTeam == nil then
		return;
	end
	self:CheckMissionSkillCost(skillTrans,missionSkillCfg,order);
end

util.hotfix_ex(CS.DeploymentSangvisSkillPanelController,'ShowSangvisSelectTarget',ShowSangvisSelectTarget)
util.hotfix_ex(CS.DeploymentSangvisSkillPanelController,'ShowVehicleSelectTarget',ShowVehicleSelectTarget)
util.hotfix_ex(CS.DeploymentSangvisSkillPanelController,'RefreshVehicleSkill1',RefreshVehicleSkill1)
util.hotfix_ex(CS.DeploymentSangvisSkillPanelController,'RefreshVehicleSkill2',RefreshVehicleSkill2)
util.hotfix_ex(CS.DeploymentSangvisSkillPanelController,'RefreshVehicleSkill3',RefreshVehicleSkill3)
util.hotfix_ex(CS.DeploymentSangvisSkillPanelController,'RefreshSangvisSkill3',RefreshSangvisSkill3)
util.hotfix_ex(CS.DeploymentSangvisSkillPanelController,'CheckMissionSkillCost',CheckMissionSkillCost)
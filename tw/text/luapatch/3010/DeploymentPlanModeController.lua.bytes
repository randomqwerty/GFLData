local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentPlanModeController)
xlua.private_accessible(CS.DeploymentPlanModeController.Plan)
--修正计划移动线层级
local CheckData = function(self)
	self:CheckData();
	local moveline= CS.DeploymentBackgroundController.Instance.transform:Find("Active/MoveLines");
	local canvas = moveline:GetComponent(typeof(CS.UnityEngine.Canvas));
	local spotparent = CS.DeploymentBackgroundController.currentLayerData.spotsParent;
	local spotCanvas = spotparent.transform:GetComponent(typeof(CS.UnityEngine.Canvas));
	canvas.sortingOrder = spotCanvas.sortingOrder;
end

local OnClickFastSelect = function(self,on)
	
end

local StartPlan = function(self)
	if CS.DeploymentBuildSkillItem.currentSkillItem ~= nil then
		CS.DeploymentBuildSkillItem.currentSkillItem:CloseAllSelectTarget();
	end
	self:StartPlan();
end

local _CancelPlan = function(self)
	if CS.GameData.missionAction ~= nil then
		if CS.GameData.missionAction.currentTurnBelong ~= CS.MissionAction.TurnBelong.SelfTurn then
			self:Clear();
			self:UpdateRecordMask();
			self:UpdatePlanMark();
			self.status = CS.DeploymentPlanModeController.PlanStatus.normal;
			CS.DeploymentUIController.Instance:ShowHideButton(true);
			CS.DeploymentController.TriggerSwitchAbovePanelEvent(true);
		else
			self:_CancelPlan();
		end
	end
	self:StopAllCoroutines();
end


local DequeueAndPlay = function(self)
	if CS.DeploymentController.Instance ~= nil then
		if CS.DeploymentController.Instance._randomEventController ~= nil then
			self:DequeueAndPlay();
			return;
		end
	end
	if CS.GameData.engagedSpot ~= nil then
		return;
	end
	self:DequeueAndPlay();
end
local Play = function(self)
	if CS.GameData.engagedSpot ~= nil then
		return;
	end
	self:Play();
end
--util.hotfix_ex(CS.DeploymentPlanModeController,'CheckData',CheckData)
--util.hotfix_ex(CS.DeploymentPlanModeController,'OnClickFastSelect',OnClickFastSelect)
--util.hotfix_ex(CS.DeploymentPlanModeController,'StartPlan',StartPlan)
util.hotfix_ex(CS.DeploymentPlanModeController,'_CancelPlan',_CancelPlan)
util.hotfix_ex(CS.DeploymentPlanModeController,'DequeueAndPlay',DequeueAndPlay)
util.hotfix_ex(CS.DeploymentPlanModeController,'Play',Play)
--util.hotfix_ex(CS.DeploymentPlanModeController.Plan,'Play',Play)



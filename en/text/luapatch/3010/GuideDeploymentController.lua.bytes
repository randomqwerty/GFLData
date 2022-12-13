local util = require 'xlua.util'
xlua.private_accessible(CS.GuideDeploymentController)
--修正显示层级
local get_Instance = function()
	local instance = CS.GuideDeploymentController.Instance;
	local canvas = instance.gameObject:GetComponent(typeof(CS.UnityEngine.Canvas));
	canvas.sortingOrder = 35;
	return  instance;
end
local check = false;
--修正下一步提前触发导致的问题
local AfterBattlePlay = function(handle)
	CS.GuideDeploymentController.AfterBattlePlay(handle);
	check = true;
end

local PlayCurrentDelay = function()
	CS.GuideDeploymentController.PlayCurrentDelay();
	CS.DeploymentController.Instance:AddAndPlayPerformance(nil);
end

local CheckStep = function()
	CS.DeploymentController.Instance:AddAndPlayPerformance(PlayCurrentDelay);
end

local PlayCurrentStep = function()
	CS.GuideDeploymentController.findObj = nil;
	CS.GuideDeploymentController.canClickOther = false;
	CS.GuideDeploymentController.Instance.above.gameObject:SetActive(true);
	CS.DeploymentController.AddAction(CheckStep,0.5);
	if check then
		check = false;
		CS.DeploymentController.Instance:AddAndPlayPerformance(nil);
	end
end

local FinishCurrentStep = function(self)
	if CS.GuideDeploymentController.currentGuideStep == nil then
		return;
	end
	self:FinishCurrentStep();
end

local ClearGuideData = function()
	CS.GuideDeploymentController.ClearGuideData();
	CS.GuideDeploymentController.canClickOther = true;
end

local SkipCompleteCurrentGuide = function(self)
	self:SkipCompleteCurrentGuide();
	CS.GuideDeploymentController.canClickOther = true;
end
util.hotfix_ex(CS.GuideDeploymentController,'get_Instance',get_Instance)
util.hotfix_ex(CS.GuideDeploymentController,'AfterBattlePlay',AfterBattlePlay)
util.hotfix_ex(CS.GuideDeploymentController,'PlayCurrentStep',PlayCurrentStep)
util.hotfix_ex(CS.GuideDeploymentController,'PlayCurrentDelay',PlayCurrentDelay)
util.hotfix_ex(CS.GuideDeploymentController,'FinishCurrentStep',FinishCurrentStep)
util.hotfix_ex(CS.GuideDeploymentController,'ClearGuideData',ClearGuideData)
util.hotfix_ex(CS.GuideDeploymentController,'SkipCompleteCurrentGuide',SkipCompleteCurrentGuide)


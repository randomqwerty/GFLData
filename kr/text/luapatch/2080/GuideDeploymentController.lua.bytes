local util = require 'xlua.util'
xlua.private_accessible(CS.GuideDeploymentController)
xlua.private_accessible(CS.DeploymentController)

canClick = true;
local CheckAbove = function()
	local above = CS.GuideDeploymentController.Instance.transform:Find("Img_Cover");
	if above ~= nil then
		print("关闭cover")
		canClick = true;
		above.gameObject:SetActive(false);
		local map = CS.DeploymentBackgroundController.Instance.transform:Find("CanvasMap");
		local active = CS.DeploymentBackgroundController.Instance.transform:Find("Active");
		map:GetComponent(typeof(CS.UnityEngine.UI.GraphicRaycaster)).enabled  = true;
		active:GetComponent(typeof(CS.UnityEngine.UI.GraphicRaycaster)).enabled  = true;	
	end	
end

local PlayCurrentDelay = function()
	CS.GuideDeploymentController.PlayCurrentDelay();
	CS.DeploymentController.AddAction(CheckAbove, 0.8);
end

local PlayCurrentStep = function()
	local above = CS.GuideDeploymentController.Instance.transform:Find("Img_Cover");
	if above ~= nil then
		canClick = false;
		above.gameObject:SetActive(true);
		local map = CS.DeploymentBackgroundController.Instance.transform:Find("CanvasMap");
		local active = CS.DeploymentBackgroundController.Instance.transform:Find("Active");
		map:GetComponent(typeof(CS.UnityEngine.UI.GraphicRaycaster)).enabled  = false;
		active:GetComponent(typeof(CS.UnityEngine.UI.GraphicRaycaster)).enabled  = false;		
	end
	CS.DeploymentController.Instance:AddAndPlayPerformance(nil);
	CS.GuideDeploymentController.PlayCurrentStep();
end

local AfterBattlePlay = function(self,handle)
	self.finishStephandle = handle;
	if self.finishStephandle ~= nil then
		self:finishStephandle();
		self.finishStephandle = nil;
	end
	CS.DeploymentController.Instance:AddAndPlayPerformance(PlayCurrentStep);
end

local CanTriggerGuide = function(self,guideData,condition,a,b)
	local hascondition = CS.System.Collections.Generic.List(CS.System.Int32)();
	for i=0,guideData.guideTriggerDataOr.Count-1 do
		local orData = guideData.guideTriggerDataOr[i];
		for j=0,orData.guideTriggerDataAnd.Count-1 do
			local data = orData.guideTriggerDataAnd[j];
			if data.trigger == condition then
				if not hascondition:Contains(i) then
					hascondition:Add(i);
				end
			end
		end
	end
	if hascondition.Count>0 then
		for i=0,hascondition.Count-1 do
			local result = true;
			for j=0,guideData.guideTriggerDataOr[hascondition[i]].guideTriggerDataAnd.Count-1 do
				local data = guideData.guideTriggerDataOr[hascondition[i]].guideTriggerDataAnd[j];
				if data.trigger == condition then
					result = result and self:CanTriggerEvent(data, a, b);
				else
					result = result and self:CanTriggerState(data);
				end
			end
			if result then
				return true;
			end
		end
		return false;
	end
	return false;
end

local CheckTime = function(self)
	self:CheckTime();
	if not self.picImage.gameObject.activeInHierarchy and not self.imageDialog.gameObject.activeInHierarchy and not self.guideImagePage.gameObject.activeInHierarchy then
		self:FinishCurrentStep();
	end
end


local CheckCurrentGuideStep = function(self)

end

local FinishCurrentStep = function()
	CS.GuideDeploymentController.Instance:FinishCurrentStep();
end
local SelectSpot = function(self,spotid)
	local spot = CS.DeploymentBackgroundController.Instance.listSpot:GetDataById(spotid);
	if spot ~= nil and spot.currentHostage ~= nil then
		print("check")
		spot.currentHostage.onClickGuideHandle = FinishCurrentStep;
	end
	return self:SelectSpot(spotid);
end
local SkipCurrentGuidegroup = function(self)
	self:FinishCurrentGuide();
	self.btnSkip.onClick:RemoveAllListeners();
end

local TriggerGuide = function(self,condition,a,b)
	if CS.GameData.missionAction.queuePerformanceHandler.Count>0 then
		print("正在播放演出")
		return;
	end
	self:TriggerGuide(condition,a,b);
end

local CheckPathObjActive = function(path)
	local text = Split(path,"/");
	if text[1] ~= nil then
		local obj = CS.UnityEngine.GameObject.Find(text[1]);
		if obj ~= nil and text[2] ~= nil then
			local child = obj.transform:Find(text[2]);
			if child ~= nil then
				return  child.gameObject;
			end
		end
		return obj;
	end
	return nil;
end

function Split(szFullString, szSeparator)
	local nFindStartIndex = 1
	local nSplitIndex = 1
	local nSplitArray = {}
	while true do
		local nFindLastIndex = string.find(szFullString, szSeparator, nFindStartIndex)
		if not nFindLastIndex then
			nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, string.len(szFullString))
			break
		end
		nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, nFindLastIndex - 1)
		nFindStartIndex = nFindLastIndex + string.len(szSeparator)
		nSplitIndex = nSplitIndex + 1
	end
	return nSplitArray
end

util.hotfix_ex(CS.GuideDeploymentController,'CheckCurrentGuideStep',CheckCurrentGuideStep)
util.hotfix_ex(CS.GuideDeploymentController,'CheckTime',CheckTime)
util.hotfix_ex(CS.GuideDeploymentController,'AfterBattlePlay',AfterBattlePlay)
util.hotfix_ex(CS.GuideDeploymentController,'PlayCurrentStep',PlayCurrentStep)
util.hotfix_ex(CS.GuideDeploymentController,'PlayCurrentDelay',PlayCurrentDelay)
util.hotfix_ex(CS.GuideDeploymentController,'CanTriggerGuide',CanTriggerGuide)
util.hotfix_ex(CS.GuideDeploymentController,'SelectSpot',SelectSpot)
util.hotfix_ex(CS.GuideDeploymentController,'SkipCurrentGuidegroup',SkipCurrentGuidegroup)
--util.hotfix_ex(CS.GuideDeploymentController,'TriggerGuide',TriggerGuide)
--util.hotfix_ex(CS.GuideDeploymentController,'CheckPathObjActive',CheckPathObjActive)

local util = require 'xlua.util'
xlua.private_accessible(CS.GuideDeploymentController)

function CheckFinishCurrentStep()
	CS.GuideDeploymentController.Instance:FinishCurrentStep();
end

function CheckFinishCurrentStepToogle(select)
	CS.GuideDeploymentController.Instance:FinishCurrentStepToogle(select);
end

local SelectButton = function(self)
	local currentGuideStep = CS.GuideDeploymentController.currentGuideStep;
	local obj = self:CheckFindbuttonOrToggle();
	if obj == nil then
		CS.NDebug.LogBlue("当前未找到对象", currentGuideStep.path,"请设置上层激活条件对象");
		return false;
	end
	if not obj.activeInHierarchy then
		CS.NDebug.LogBlue("当前物体还未激活", obj);
		return false;
	end
	if currentGuideStep.clickType == CS.ClickType.OnClickButton then
		local btn = obj:GetComponent(typeof(CS.UnityEngine.UI.Button));
		if btn ~= nil then
			btn.onClick:AddListener(CheckFinishCurrentStep);
		end
		local toggle = obj:GetComponent(typeof(CS.UnityEngine.UI.Toggle));
		if toggle ~= nil then
			toggle.onValueChanged:AddListener(CheckFinishCurrentStepToogle);
		end
	end
	if currentGuideStep.clickType == CS.ClickType.OnClickImage then
		local btn = obj:GetComponent(typeof(CS.UnityEngine.UI.Button));
		if btn == nil then
			btn = obj:AddComponent(typeof(CS.UnityEngine.UI.Button));
		end
		btn.onClick:AddListener(CheckFinishCurrentStep);
	end
	currentGuideStep.buttonTrans = obj;
	if currentGuideStep.forceClick then
		self.target = obj:GetComponent(typeof(CS.UnityEngine.RectTransform));
		self:Mask();
		self.goMask.gameObject:SetActive(true);
	end
	if not CS.System.String.IsNullOrEmpty(currentGuideStep.uiShowPrefab) then
		CS.NDebug.LogBlue("uiShowPrefab", currentGuideStep.uiShowPrefab);
		if currentGuideStep.uiPrefab == nil or currentGuideStep.uiPrefab:isNull() then
			local prefab = CS.ResManager.GetObjectByPath("Prefabs/GuideDeployment/"..currentGuideStep.uiShowPrefab);
			if prefab ~= nil then
				currentGuideStep.uiPrefab = CS.UnityEngine.Object.Instantiate(prefab);
				if currentGuideStep.forceClick then
					currentGuideStep.uiPrefab.transform:SetParent(self.rectTransformTarget, false);
				else
					currentGuideStep.uiPrefab.transform:SetParent(obj.transform, false);
				end
			end
		end
	end
	return true;
end

local FinishCurrentStep = function(self)
	if CS.GuideDeploymentController.currentGuideStep == nil then
		return;
	end
	if CS.GuideDeploymentController.currentGuideStep.buttonTrans ~= nil then
		if CS.GuideDeploymentController.currentGuideStep.clickType == CS.ClickType.OnClickButton then
			local btn = CS.GuideDeploymentController.currentGuideStep.buttonTrans:GetComponent(typeof(CS.UnityEngine.UI.Button));
			if btn ~= nil then
				btn.onClick:RemoveListener(CheckFinishCurrentStep);
			end
			local toggle = CS.GuideDeploymentController.currentGuideStep.buttonTrans:GetComponent(typeof(CS.UnityEngine.UI.Toggle));
			if toggle ~= nil then
				toggle.onValueChanged:RemoveListener(CheckFinishCurrentStepToogle);
			end
		end
		if CS.GuideDeploymentController.currentGuideStep.clickType == CS.ClickType.OnClickImage then
			local btn = CS.GuideDeploymentController.currentGuideStep.buttonTrans:GetComponent(typeof(CS.UnityEngine.UI.Button));
			if btn ~= nil then
				btn.onClick:RemoveListener(CheckFinishCurrentStep);
			end
		end
	end
	self:FinishCurrentStep();
end
util.hotfix_ex(CS.GuideDeploymentController,'SelectButton',SelectButton)
util.hotfix_ex(CS.GuideDeploymentController,'FinishCurrentStep',FinishCurrentStep)
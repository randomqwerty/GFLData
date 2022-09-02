local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentPlanModeController)
--修正计划移动线层级
local CheckData = function(self)
	self:CheckData();
	local moveline= CS.DeploymentBackgroundController.Instance.transform:Find("Active/MoveLines");
	local canvas = moveline:GetComponent(typeof(CS.UnityEngine.Canvas));
	local spotparent = CS.DeploymentBackgroundController.currentLayerData.spotsParent;
	local spotCanvas = spotparent.transform:GetComponent(typeof(CS.UnityEngine.Canvas));
	canvas.sortingOrder = spotCanvas.sortingOrder;
end

util.hotfix_ex(CS.DeploymentPlanModeController,'CheckData',CheckData)





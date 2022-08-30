local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentUIController)

--更改遮罩层级
local Awake = function(self)
	self:Awake();
	local canvasself = self.transform:GetComponent(typeof(CS.UnityEngine.Canvas));
	local canvas = self.goAbove:GetComponent(typeof(CS.UnityEngine.Canvas));
	canvas.sortingOrder = 29;
end

--修正按钮显示
local RefreshText = function(self)
	self:RefreshText();
	if self.btnResultMission.gameObject.activeInHierarchy then
		self.btnAbortMission.gameObject:SetActive(false);
	end
end

util.hotfix_ex(CS.DeploymentUIController,'Awake',Awake)
util.hotfix_ex(CS.DeploymentUIController,'RefreshText',RefreshText)




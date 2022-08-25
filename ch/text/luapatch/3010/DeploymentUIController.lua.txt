local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentUIController)

local OnClickEndTurn = function(self)
	if CS.DeploymentController.playAniming then
		return;
	end
	self:OnClickEndTurn();
end

local Awake = function(self)
	self:Awake();
	local canvasself = self.transform:GetComponent(typeof(CS.UnityEngine.Canvas));
	local canvas = self.goAbove:GetComponent(typeof(CS.UnityEngine.Canvas));
	canvas.sortingOrder = 29;
end
util.hotfix_ex(CS.DeploymentUIController,'Awake',Awake)
util.hotfix_ex(CS.DeploymentUIController,'OnClickEndTurn',OnClickEndTurn)




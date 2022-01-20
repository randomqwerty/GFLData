local util = require 'xlua.util'
xlua.private_accessible(CS.CommonStorageFullConfirmBoxController)

local InitUI = function(self)
	self:InitUI();
	local canvas = self.gameObject:GetComponent(typeof(CS.UnityEngine.Canvas));
	canvas.sortingOrder = 31;
end
util.hotfix_ex(CS.CommonStorageFullConfirmBoxController,'InitUI',InitUI)


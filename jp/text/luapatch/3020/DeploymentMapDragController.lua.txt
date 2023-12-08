local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentMapDragController)

local CheckNext = function()
	print("PlayNext");
	CS.DeploymentController.Instance:PlayNext();
end

local ReBackView = function(self,action)
	self:ReBackView(nil);
	CS.DeploymentController.AddAction(CheckNext,1.5);
end
util.hotfix_ex(CS.DeploymentMapDragController,'ReBackView',ReBackView)
local util = require 'xlua.util'

local team = nil;
local CheckBuffUI = function()
	if team ~= nil then
		team:RefeshBuffUI();
	end
end
--修正梯队刷新只刷新Buff
local RefeshUI = function(self,delay)
	team = self.Team;
	if team ~= nil then
		CS.DeploymentController.AddAction(CheckBuffUI,delay);
	end
end

util.hotfix_ex(CS.BuffAction,'RefeshUI',RefeshUI)
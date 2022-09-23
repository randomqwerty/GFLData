local util = require 'xlua.util'
local deployment = require("3010/DeploymentController")
local missiondata = require("3010/MissionData")
--修正梯队刷新只刷新Buff
local RefeshUI = function(self,delay)
	CS.CommonController.Invoke(function()
		if self.Team ~= nil then
			self.Team:RefeshBuffUI();
		end
		end,delay,CS.DeploymentController.Instance);
end

local CheckTeamMovePlayEffect = function(self)
	self:CheckTeamMovePlayEffect();
	if self.Team ~= nil then
		showteam = self.Team;
		if playteams ~= nil then
			print(self.Team);
			playteams:Remove(self.Team);
		end
	end
	if self.build ~= nil then
		showbuild = self.build;
		if playbuilds ~= nil then
			playbuilds:Remove(self.build);
		end	
	end
	print("lastTime"..self.lastTime);
	 if effectdelaytime < self.lastTime then
	 	effectdelaytime = self.lastTime;
	 end
	print("延迟时间"..effectdelaytime);
end
util.hotfix_ex(CS.BuffAction,'RefeshUI',RefeshUI)
util.hotfix_ex(CS.HurtAction,'CheckTeamMovePlayEffect',CheckTeamMovePlayEffect)
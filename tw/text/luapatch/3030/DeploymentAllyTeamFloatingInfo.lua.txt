local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentAllyTeamFloatingInfo)

local Start = function(self)
	self:Start();
	CS.CommonController.InvokeRepeating(function()
		if self.allyTeamController ~= nil and not self.allyTeamController.currentSpot.Show then
			if self.canvasGroup.alpha>0 then
				self.canvasGroup:DOFade(0,0.5);
			end
		end
	end,0.2,0.5,self);
end
util.hotfix_ex(CS.DeploymentAllyTeamFloatingInfo,'Start',Start)
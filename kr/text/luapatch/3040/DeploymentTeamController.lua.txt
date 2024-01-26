local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamController)


local Start = function(self)
	self:Start();
	if self.leaderCharacter ~= nil then
		self.ScaleX = self.ScaleX*self.leaderCharacter.deployment_scale;
	end
	self.spineHolder.localScale = CS.UnityEngine.Vector3(self.ScaleX,self.ScaleY,self.ScaleX);
end

util.hotfix_ex(CS.DeploymentTeamController,'Start',Start)
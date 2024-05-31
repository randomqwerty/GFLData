local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentController)

local ReastSkillCD = function(self)
	self:ReastSkillCD();
	if self.currentSelectedTeam.vehicleTeam ~= nil then
		self.currentSelectedTeam.vehicleTeam.skill1cdTurn = 0;
		self.currentSelectedTeam.vehicleTeam.skill2cdTurn = 0;
		self.currentSelectedTeam.vehicleTeam.skill3cdTurn = 0;
	end
end

util.hotfix_ex(CS.DeploymentController,'ReastSkillCD',ReastSkillCD)
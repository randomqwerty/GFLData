local util = require 'xlua.util'

local PlayEffect = function(self)
	if not CS.GameData.missionAction.listSpecialSpotAction:ContainsKey(self.instanceId) then
		return;
	end
	self:PlayEffect();
end

local CheckTeamMoveDeath = function(self)
	if self.sourceType == CS.SourceType.building then
		if self.Alive then
			local buildAction = CS.GameData.missionAction.listBuildingAction:GetDataById(self.sourceValue);
			if buildAction ~= nil and buildAction.CanUseMissionSkill then
				if not buildAction.CanUseActiveMissionSkill then					
					if CS.DeploymentController.Instance ~= nil then			
						self:LastEffect();
					end
					return;
				end
			end
		end
	end
	self:CheckTeamMoveDeath();
end

local CheckTeamMoveClear = function(self)
	if self.sourceType == CS.SourceType.building then
		if self.Alive then
			local buildAction = CS.GameData.missionAction.listBuildingAction:GetDataById(self.sourceValue);
			if buildAction ~= nil and buildAction.CanUseMissionSkill then
				if not buildAction.CanUseActiveMissionSkill then
					if CS.DeploymentController.Instance ~= nil then			
						self:CheckTeamMovePlayEffect();
					end
					return;
				end
			end
		end
	end
	self:CheckTeamMoveClear();
end

util.hotfix_ex(CS.SpecialSpotAction,'PlayEffect',PlayEffect)
util.hotfix_ex(CS.SpecialSpotAction,'CheckTeamMoveDeath',CheckTeamMoveDeath)
util.hotfix_ex(CS.BuffAction,'CheckTeamMoveClear',CheckTeamMoveClear)
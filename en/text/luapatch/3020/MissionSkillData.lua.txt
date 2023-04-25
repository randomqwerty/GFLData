local util = require 'xlua.util'

local PlayEffect = function(self)
	if not CS.GameData.missionAction.listSpecialSpotAction:ContainsKey(self.instanceId) then
		return;
	end
	self:PlayEffect();
end

local RefreshUI = function(self,refreshBuffNow)
	if self.currentSpotAction.belong == CS.Belong.ingore or self.currentSpotAction.belong == CS.Belong.hide then
		return;
	end
	if self.sourceType == CS.SourceType.building and self.sourceValue ~= 0 then
		if self.Alive then
			local buildAction = CS.GameData.missionAction.listBuildingAction:GetDataById(self.sourceValue);
			if buildAction ~= nil and buildAction.CanUseMissionSkill then
				if not buildAction.CanUseActiveMissionSkill then					
					if CS.DeploymentController.Instance ~= nil then			
						self:LastEffect();
					end
					if not self.currentSpotAction.listSpecialAction:Contains(self) then
						self.currentSpotAction.listSpecialAction:Add(self);
					end
					return;
				end
			end
		end
	end
	self:RefreshUI(refreshBuffNow);
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
util.hotfix_ex(CS.SpecialSpotAction,'RefreshUI',RefreshUI)
util.hotfix_ex(CS.BuffAction,'CheckTeamMoveClear',CheckTeamMoveClear)
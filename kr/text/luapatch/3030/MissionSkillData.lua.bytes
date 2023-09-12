local util = require 'xlua.util'

local PlayEffect = function(self)
	if not CS.GameData.missionAction.listSpecialSpotAction:ContainsKey(self.instanceId) then
		return;
	end
	if self.sourceType == CS.SourceType.building and self.sourceValue ~= 0 then
		local buildAction = CS.GameData.missionAction.listBuildingAction:GetDataById(self.sourceValue);
		if buildAction ~= nil then
			self.sourceSpotAction = buildAction.currentSpotAction;
		end
	end
	self:PlayEffect();
end

local RefreshUI = function(self,refreshBuffNow)
	if self.currentSpotAction.belong == CS.Belong.ingore or self.currentSpotAction.belong == CS.Belong.hide then
		return;
	end
	if not self.currentSpotAction.listSpecialAction:Contains(self) then
		self.currentSpotAction.listSpecialAction:Add(self);
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
			if buildAction == nil then
				return;
			end
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

local CheckNext = function()
	print("PlayNext");
	CS.DeploymentController.Instance:PlayNext();
end
local delay = 0;
local DelayPerformance = function()
	print("插入延时");
	CS.DeploymentController.AddAction(CheckNext,delay);
end

local AddDelayPerformance = function()
	CS.DeploymentController.Instance:AddAndPlayPerformance(DelayPerformance);
end		
local ShowEffect = function(target,effectInfo,autoDestroy,effectObj,lastdelayTime,playsound)
	if effectInfo.cameraFollowEffect then
		delay = lastdelayTime+effectInfo.forceDelay+effectInfo.forceLastTime;
		print("插入队列延时"..tostring(delay));
		CS.DeploymentController.Instance:InsertSomePlayPerformances(AddDelayPerformance);
	end
	effectObj = CS.SpecialSpotAction.ShowEffect(target,effectInfo,autoDestroy,effectObj,lastdelayTime,playsound);
	return effectObj;
end
local LoadHurtData = function(self)
	--print("LoadHurtData")
	local sangvisteamid = self.sangvisTeamId;
	self.sangvisTeamId = 0;
	self:LoadHurtData();
	self.sangvisTeamId = sangvisteamid;
	if sangvisteamid ~= 0 then
		local gunJson = self.jsonData:GetValue("sangvises_life");
		for i=0,gunJson.Count-1 do
			local gunid = gunJson[i]:GetValue("sangvis_with_user_id").Long;
			local life = gunJson[i]:GetValue("life").Int;
			local gun = CS.GameData.listSangvisGun:GetDataById(gunid);
			if life>gun.life then
				self.playHurt = false;
			end
			gun.life = life;
		end
		if self.Team ~= nil then
			self.Team:RefreshTeamInfo();
		end
	end
end
util.hotfix_ex(CS.SpecialSpotAction,'PlayEffect',PlayEffect)
util.hotfix_ex(CS.SpecialSpotAction,'RefreshUI',RefreshUI)
util.hotfix_ex(CS.SpecialSpotAction,'ShowEffect',ShowEffect)
util.hotfix_ex(CS.BuffAction,'CheckTeamMoveClear',CheckTeamMoveClear)
util.hotfix_ex(CS.HurtAction,'LoadHurtData',LoadHurtData)
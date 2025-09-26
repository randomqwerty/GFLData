local util = require 'xlua.util'
xlua.private_accessible(CS.HurtAction)
xlua.private_accessible(CS.MissionAction)
local PlayEffect = function(self)
	if self.Team == nil then
		--CS.NDebug.LogError("缺少Team",self.teamType);
		return;
	end
	self:PlayEffect();
end
local PlayHurtEffect = function(self)
	self:PlayEffect();
	CS.GameData.missionAction.playHurtAction:Remove(self);
end
local ReadFriendSkillData = function(self,id,spotid)
	if self.friendTeamData:ContainsKey(id) then
		if self.friendTeamData[id]:ContainsKey(spotid) then
			local hurtaction = CS.HurtAction(self.friendTeamData[id][spotid]);
			self.friendTeamData[id]:Remove(spotid);
			if not hurtaction:HasTeamTrans() and not hurtaction:HasTeamMove() then
				hurtaction:PlayEffect();
			end
		end
	end
end
local ReadEnemySkillData = function(self,id,spotid)
	if self.enemyTeamData:ContainsKey(id) then
		if self.enemyTeamData[id]:ContainsKey(spotid) then
			local hurtaction = CS.HurtAction(self.enemyTeamData[id][spotid]);
			self.enemyTeamData[id]:Remove(spotid);
			if not hurtaction:HasTeamTrans() and not hurtaction:HasTeamMove() then
				hurtaction:PlayEffect();
			end
		end
	end
end
local ReadAllySkillData = function(self,id,spotid)
	if self.allyTeamData:ContainsKey(id) then
		if self.allyTeamData[id]:ContainsKey(spotid) then
			local hurtaction = CS.HurtAction(self.allyTeamData[id][spotid]);
			self.allyTeamData[id]:Remove(spotid);
			if not hurtaction:HasTeamTrans() and not hurtaction:HasTeamMove() then
				hurtaction:PlayEffect();
			end
		end
	end
end
local ReadSquadSkillData = function(self,id,spotid)
	if self.squadTeamData:ContainsKey(id) then
		if self.squadTeamData[id]:ContainsKey(spotid) then
			local hurtaction = CS.HurtAction(self.squadTeamData[id][spotid]);
			self.squadTeamData[id]:Remove(spotid);
			if not hurtaction:HasTeamTrans() and not hurtaction:HasTeamMove() then
				hurtaction:PlayEffect();
			end
		end
	end
end
local ReadVehicleSkillData = function(self,id,spotid)
	if self.vehicleTeamData:ContainsKey(id) then
		if self.vehicleTeamData[id]:ContainsKey(spotid) then
			local hurtaction = CS.HurtAction(self.vehicleTeamData[id][spotid]);
			self.vehicleTeamData[id]:Remove(spotid);
			if not hurtaction:HasTeamTrans() and not hurtaction:HasTeamMove() then
				hurtaction:PlayEffect();
			end
		end
	end
end
local ReadSangvisSkillData = function(self,id,spotid)
	if self.sangvisTeamData:ContainsKey(id) then
		if self.sangvisTeamData[id]:ContainsKey(spotid) then
			local hurtaction = CS.HurtAction(self.sangvisTeamData[id][spotid]);
			self.sangvisTeamData[id]:Remove(spotid);
			if not hurtaction:HasTeamTrans() and not hurtaction:HasTeamMove() then
				hurtaction:PlayEffect();
			end
		end
	end
end
local isFriendFairyTeamSource = function(sourceType)
	if sourceType == CS.SourceType.fairy then
		return true;
	end
	return false;
end
local LoadFairySkillPerform = function(self,jsonData,readObject)
	util.hotfix_ex(CS.MissionSkill,'isFriendTeamSource',isFriendFairyTeamSource)
	self:LoadFairySkillPerform(jsonData,readObject);
	xlua.hotfix(CS.MissionSkill,'isFriendTeamSource',nil)
end
util.hotfix_ex(CS.BuffAction,'PlayEffect',PlayEffect)
util.hotfix_ex(CS.HurtAction,'PlayEffect',PlayHurtEffect)
util.hotfix_ex(CS.MissionAction,'ReadFriendSkillData',ReadFriendSkillData)
util.hotfix_ex(CS.MissionAction,'ReadEnemySkillData',ReadEnemySkillData)
util.hotfix_ex(CS.MissionAction,'ReadAllySkillData',ReadAllySkillData)
util.hotfix_ex(CS.MissionAction,'ReadSquadSkillData',ReadSquadSkillData)
util.hotfix_ex(CS.MissionAction,'ReadVehicleSkillData',ReadVehicleSkillData)
util.hotfix_ex(CS.MissionAction,'ReadSangvisSkillData',ReadSangvisSkillData)
util.hotfix_ex(CS.MissionAction,'LoadFairySkillPerform',LoadFairySkillPerform)
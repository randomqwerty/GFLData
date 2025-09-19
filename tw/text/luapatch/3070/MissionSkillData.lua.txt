local util = require 'xlua.util'
xlua.private_accessible(CS.BuffAction)
xlua.private_accessible(CS.MissionAction)
local LastEffect = function(self,delay)
	if self.Team == nil then
		return; 
	end
	if self.Team.spineHolder == nil then
		return;
	end
	self:LastEffect(delay);
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
util.hotfix_ex(CS.BuffAction,'LastEffect',LastEffect)
util.hotfix_ex(CS.MissionAction,'LoadFairySkillPerform',LoadFairySkillPerform)
local util = require 'xlua.util'
xlua.private_accessible(CS.DeploymentTeamController)

local ShowHaloSkill = function(self,Iconfriendly,num)
	self:ShowHaloSkill(Iconfriendly,num);
	if self.holeShow ~= nil then
		local canvas = self.holeShow:GetComponent(typeof(CS.UnityEngine.Canvas));
		if canvas == nil or canvas:isNull() then
			self.holeShow:AddComponent(typeof(CS.UnityEngine.Canvas));
		end
	end
end

local ShowBattleSkill = function(self,Iconfriendly,num)
	self:ShowBattleSkill(Iconfriendly,num);
	if self.SkillShow ~= nil then
		local canvas = self.SkillShow:GetComponent(typeof(CS.UnityEngine.Canvas));
		if canvas == nil or canvas:isNull() then
			self.SkillShow:AddComponent(typeof(CS.UnityEngine.Canvas));
		end
	end
end
util.hotfix_ex(CS.DeploymentTeamController,'ShowHaloSkill',ShowHaloSkill)
util.hotfix_ex(CS.DeploymentTeamController,'ShowBattleSkill',ShowBattleSkill)
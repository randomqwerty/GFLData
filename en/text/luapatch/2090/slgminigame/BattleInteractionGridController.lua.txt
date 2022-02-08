local util = require 'xlua.util'
xlua.private_accessible(CS.BattleInteractionGridController)
local flatSkillCancelFlag = false
local flatSkillCancelCounter = 0
local SLGShow = function(self,isBlocked)
	self:SLGShow(isBlocked)
	if self:GetComponent(typeof(CS.UnityEngine.BoxCollider)) ~= nil then
		self:GetComponent(typeof(CS.UnityEngine.BoxCollider)).center = CS.UnityEngine.Vector3(-0.81,0,0.1)
	end
end

util.hotfix_ex(CS.BattleInteractionGridController,'SLGShow',SLGShow)


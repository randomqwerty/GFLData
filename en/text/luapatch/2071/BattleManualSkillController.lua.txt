local util = require 'xlua.util'
xlua.private_accessible(CS.BattleManualSkillController)

local Init = function(self,characterId,chara,sangvisUsingSkill)

	self:Init(characterId,chara,sangvisUsingSkill)
	self.animCDDone.gameObject:GetComponent(typeof(CS.UnityEngine.SpriteRenderer)).material:SetFloat("ZWrite",0)
end

util.hotfix_ex(CS.BattleManualSkillController,'Init',Init)

local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.CSkillManager)
local UninitSkill = function(self)
	self:UninitSkill()
	CS.BattleFrameManager.Instance.battleFrameScale = 1
	CS.UnityEngine.Time.timeScale = 1
end
util.hotfix_ex(CS.GF.Battle.CSkillManager,'UninitSkill',UninitSkill)
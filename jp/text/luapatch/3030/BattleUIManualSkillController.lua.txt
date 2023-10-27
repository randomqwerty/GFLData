local util = require 'xlua.util'

xlua.private_accessible(CS.BattleUIManualSkillController)

local ActiveSkill = function(self,sender,e)
	self.listManualSkillController = CS.BattleUIManualSkillController.Instance.listManualSkillController
	self:ActiveSkill(sender,e)
end
util.hotfix_ex(CS.BattleUIManualSkillController,'ActiveSkill',ActiveSkill)
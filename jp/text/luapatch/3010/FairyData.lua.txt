local util = require 'xlua.util'
xlua.private_accessible(CS.Fairy)
local get_autoSkill = function(self)
	if self.isFriendFairy then
		return false;
	end
	return self:LoadFairySkillState();
end
util.hotfix_ex(CS.Fairy,'get_autoSkill',get_autoSkill)
local util = require 'xlua.util'
xlua.private_accessible(CS.BattleSkillTipItem)

local InitData = function(self,skillType,desc)
	if CS.HotUpdateController.instance.mUsePlatform == CS.HotUpdateController.EUsePlatform.ePlatform_US then
		self.txtDesc.isOrnamental = false;
	end
	self:InitData(skillType,desc);
	self.txtDesc.gameObject:SetActive(true);
end

util.hotfix_ex(CS.BattleSkillTipItem,'InitData',InitData)


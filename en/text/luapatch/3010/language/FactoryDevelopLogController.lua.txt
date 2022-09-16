local util = require 'xlua.util'
xlua.private_accessible(CS.FactoryController)

local FactoryDevelopInitUIElements = function(self)
    self:InitUIElements()
	self.header5.text = CS.Data.GetLang(32325)
end

local OrganizationSkillInitUIElements = function(self)
	self:InitUIElements()
	self.btnGetAll.gameObject:GetComponentInChildren(typeof(CS.ExText)).text = CS.Data.GetLang(1766)
	self.transform:Find("Middle/Content/Holder/Get/Btn_Get/Tex_Get").gameObject:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(1157)
	self.transform:Find("Middle/Content/Holder/Get/Btn_UnGet/Tex_UnGet").gameObject:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(1157)
end


local OrganizationDetailInitUIElements = function(self)
	self:InitUIElements()
	self.objMaxExp:GetComponent(typeof(CS.ExText)).text = CS.Data.GetLang(130057)
end

--util.hotfix_ex(CS.FactoryDevelopLogController,'InitUIElements',FactoryDevelopInitUIElements)
--util.hotfix_ex(CS.OrganizationSkillsRewardController,'InitUIElements',OrganizationSkillInitUIElements)
--util.hotfix_ex(CS.OrganizationDepDetail,'InitUIElements',OrganizationDetailInitUIElements)
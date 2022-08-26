local util = require 'xlua.util'
xlua.private_accessible(CS.IllusBookEquipSuitCtrl)
xlua.private_accessible(CS.IllusBookEquipListLableCtrl)
--xlua.private_accessible(CS.EquipInfo)
local _BackGroundColor = function(self)
	if CS.IllusBookEquipListCtrl.Instance ~= nil then
		local index = CS.System.Convert.ToInt32(self.equipInfo.rank); 
		self.picBackground.sprite = CS.IllusBookEquipListCtrl.Instance.arrImageRankBackground[ index - 2];
	end
end
local _InitIllusbook = function(self,group_id) 
	xlua.hotfix(CS.IllusBookEquipListLableCtrl,'BackGroundColor',_BackGroundColor)
	self:InitIllusbook(group_id); 
end
local _InitSkillInfo = function(self) 
	xlua.hotfix(CS.IllusBookEquipListLableCtrl,'BackGroundColor',nil)
	self:InitSkillInfo(); 
end
util.hotfix_ex(CS.IllusBookEquipSuitCtrl,'InitIllusbook',_InitIllusbook)
util.hotfix_ex(CS.IllusBookEquipSuitCtrl,'InitSkillInfo',_InitSkillInfo)


local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisLeaderLabelController)

local OpenChipList = function(self,index)
	if not CS.GameData.listSangvisGun:Contains(self.gun) then
		CS.CommonController.LightMessageTips(CS.Data.GetLang(33060));
		return; 
	end
	self:OpenChipList(index);
end

util.hotfix_ex(CS.SangvisLeaderLabelController,'OpenChipList',OpenChipList)



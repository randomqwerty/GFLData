local util = require 'xlua.util'
xlua.private_accessible(CS.CommonCharacterListController)
--拆解列表剔除掉已编入载具的人形
local _GunFilter = function(self,g)
	if self.listType == CS.ListType.feed or self.listType == CS.ListType.retire then
		if g.vehicleId ~= 0 then
			return false;
		end
	end
	return self:GunFilter(g);
end

util.hotfix_ex(CS.CommonCharacterListController,'GunFilter',_GunFilter)
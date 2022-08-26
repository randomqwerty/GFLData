local util = require 'xlua.util'
xlua.private_accessible(CS.ItemPackage)

local CanGetAmount = function(self,allowlimit)
	if self.info == nil then
		print("缺少ItemInfo");
		return self.amount;
	end
	if CS.GameData.itemLimit == nil then
		if allowlimit and self.info.upper_limit ~= 0 then
			local canget = CS.Mathf.Max(0, self.info.upper_limit - CS.GameData.GetItem(self.info.itemId));
			return CS.Mathf.Min(canget, self.amount);
		end
		return self.amount;
	end
	return self:CanGetAmount(allowlimit);
end

util.hotfix_ex(CS.ItemPackage,'CanGetAmount',CanGetAmount)




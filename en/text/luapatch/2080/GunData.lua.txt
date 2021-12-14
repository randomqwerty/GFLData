local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.Gun)

local code = function(self)
	if self.allyGunInfo ~= nil then
		self.info.maxMod = CS.Mathf.Max(self.info.maxMod, self.allyGunInfo.mod);
	end
	return self.code;
end

util.hotfix_ex(CS.GF.Battle.Gun,'get_code',code)




local util = require 'xlua.util'
xlua.private_accessible(CS.Mission)
local UseWinCounter = function(self)
	if self.missionInfo.isEndless then
		return self.counter;
	end
	return self.UseWinCounter;
end
util.hotfix_ex(CS.Mission,'get_UseWinCounter',UseWinCounter)

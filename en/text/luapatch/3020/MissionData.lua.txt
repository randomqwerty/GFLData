local util = require 'xlua.util'
xlua.private_accessible(CS.Mission)
xlua.private_accessible(CS.SpotAction)
local UseWinCounter = function(self)
	if self.missionInfo.isEndless then
		return self.counter;
	end
	return self.UseWinCounter;
end
local teamEchelon = function(self)
	if self.HasTeam and not self.hasFriendTeam then
		if self.spot~= nil and not self.spot.Show then
			return 0;
		end
	end
	return self.teamEchelon;
end
util.hotfix_ex(CS.Mission,'get_UseWinCounter',UseWinCounter)
util.hotfix_ex(CS.SpotAction,'get_teamEchelon',teamEchelon)

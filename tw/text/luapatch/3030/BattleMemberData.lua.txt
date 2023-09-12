local util = require 'xlua.util'
xlua.private_accessible(CS.GF.Battle.BattleMemberData)

local GetSpineActionFrame = function(self,name)
	local t = self:GetSpineActionFrame(name)
	return self:GetSpineActionFrame(name)
end

util.hotfix_ex(CS.GF.Battle.BattleMemberData,'GetSpineActionFrame',GetSpineActionFrame)
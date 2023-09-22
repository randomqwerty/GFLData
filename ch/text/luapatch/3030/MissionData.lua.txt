local util = require 'xlua.util'

local InitData = function(self)	
	self:InitData();
	if not CS.System.String.IsNullOrEmpty(self.limit_team) then
		local txt = Split(self.limit_team,",");
		for j=1,#txt do			
			local mtxt = txt[j];
			if j == 2 then
				if string.find(mtxt, "*") == 1 then	
					mtxt = string.sub(mtxt, 2);
				end	
				self.basetotalTeamLimit	= tonumber(mtxt);
			end
		end
	end
end

function Split(szFullString, szSeparator)
	local nFindStartIndex = 1
	local nSplitIndex = 1
	local nSplitArray = {}
	while true do
		local nFindLastIndex = string.find(szFullString, szSeparator, nFindStartIndex)
		if not nFindLastIndex then
			nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, string.len(szFullString))
			break
		end
		nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, nFindLastIndex - 1)
		nFindStartIndex = nFindLastIndex + string.len(szSeparator)
		nSplitIndex = nSplitIndex + 1
	end
	return nSplitArray
end

util.hotfix_ex(CS.MissionInfo,'InitData',InitData)

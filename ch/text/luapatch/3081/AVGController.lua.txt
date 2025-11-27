local util = require 'xlua.util'
xlua.private_accessible(CS.AVGController)

local lineTable = {};
local WriteEffectToLineData = function(self,aVGControllerEffect,currentLine,effectTag1,effectTag2,typeId,type,isDelayOrSpeed)
	self:WriteEffectToLineData(aVGControllerEffect,currentLine,effectTag1,effectTag2,typeId,type,isDelayOrSpeed);
	if type == CS.AVGEffectType.Credits2 then
		lineTable[currentLine] = self.avgCreditsName;
	end
end
local PlayOneLine = function(self)
	local line = self.currentNode.Value;
	if lineTable[line] ~= nil then
		self.avgCreditsName = lineTable[line];
	end
	self:PlayOneLine();
end
util.hotfix_ex(CS.AVGController,'WriteEffectToLineData',WriteEffectToLineData)
util.hotfix_ex(CS.AVGController,'PlayOneLine',PlayOneLine)
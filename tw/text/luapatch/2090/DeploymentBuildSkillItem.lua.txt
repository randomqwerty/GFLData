local util = require 'xlua.util'
xlua.private_accessible(CS.BuildSkillDetail)

local RequestControlBuild = function(self,data)
	if self.skillItem~=nil and self.skillItem.missionskillinfo ~= nil and self.skillItem.missionskillinfo.apCost>0 then
		--print(self.skillItem.missionskillinfo.apCost);
		CS.GameData.missionAction.ap =CS.GameData.missionAction.ap-self.skillItem.missionskillinfo.apCost;
	end
	self:RequestControlBuild(data);
end


util.hotfix_ex(CS.BuildSkillDetail,'RequestControlBuild',RequestControlBuild)




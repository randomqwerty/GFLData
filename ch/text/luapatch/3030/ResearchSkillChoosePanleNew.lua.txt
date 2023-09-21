local util = require 'xlua.util'
xlua.private_accessible(CS.ResearchSkillChoosePanleNew)

local _SangvisSkillNextLevelInfo = function(self,sangvisSkillInfo,addLevel)
	local isMax = self:isSkillLevelMax(self.skillIndex);
	if isMax == true then
		 self.texLevelNextPrent:SetActive(false);
		 self:RefreshSkillUpdateInfo(sangvisSkillInfo.lvInfos, nil, true);
	else
		self:SangvisSkillNextLevelInfo(sangvisSkillInfo,addLevel);
	end
end
util.hotfix_ex(CS.ResearchSkillChoosePanleNew,'SangvisSkillNextLevelInfo',_SangvisSkillNextLevelInfo)
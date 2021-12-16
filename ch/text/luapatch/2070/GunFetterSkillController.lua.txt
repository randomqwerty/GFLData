local util = require 'xlua.util'
xlua.private_accessible(CS.GunFetterSkillController)

local _InitUIElements = function(self)
	self:InitUIElements();
	self.title.resizeTextForBestFit=true;
end
local _UpdateHeader = function(self)
	self:UpdateHeader();
	local count=self.listSkillObj.Count-1;
	for i=0,count,1 do
		local text1 =self.listSkillObj[i].transform:Find("FetterSkillName/Tex_SkillName"):GetComponent(typeof(CS.ExText));
		text1.resizeTextForBestFit=true;	 
	end 
end

util.hotfix_ex(CS.GunFetterSkillController,'InitUIElements',_InitUIElements)
util.hotfix_ex(CS.GunFetterSkillController,'UpdateHeader',_UpdateHeader)

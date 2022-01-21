local util = require 'xlua.util'
xlua.private_accessible(CS.SquadChipListLabelController)

local _Awake = function(self)
	self:Awake();
	if self.gobjPreviewNode~=nil then
		local txt1 = self.gobjPreviewNode.transform:Find("Tex_MaxLVPreview"):GetComponent(typeof(CS.ExText));
		txt1.text = CS.Data.GetLang(190266);
	end
end

util.hotfix_ex(CS.SquadChipListLabelController,'Awake',_Awake)
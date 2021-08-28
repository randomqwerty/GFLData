local util = require 'xlua.util'

xlua.private_accessible(CS.CommonCharacterListLabelControler)
local Awake_New = function(self)
	if self.imageSkill1Icon ~= nil then
		self.imageSkill1Icon.transform.parent.gameObject:SetActive(false);
	end

	if self.imageSkill2Icon ~= nil then
		self.imageSkill2Icon.transform.parent.gameObject:SetActive(false);
	end

	--CS.NDebug.LogError("Awake_New")
end

util.hotfix_ex(CS.CommonCharacterListLabelControler,'Awake',Awake_New)






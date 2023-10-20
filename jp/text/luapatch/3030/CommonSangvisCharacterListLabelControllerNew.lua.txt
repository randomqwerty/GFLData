local util = require 'xlua.util'
xlua.private_accessible(CS.CommonSangvisCharacterListLabelControllerNew)

local _get_listType = function(self)
	if self.parentController ~= nil then
		return self.parentController.currentSetting.listType;
	else
		return CS.CommonSangvisCharacterListController.ListType.FormationLeader;
	end
end
util.hotfix_ex(CS.CommonSangvisCharacterListLabelControllerNew,'get_listType',_get_listType)
local util = require 'xlua.util'
xlua.private_accessible(CS.CommonCharacterListLabelControler)
local get_isSimFormation = function(self)
	return self.listType == CS.ListType.simulator or self.listType == CS.ListType.theater or self.listType == CS.ListType.theateAlterFormation; 
end
util.hotfix_ex(CS.CommonCharacterListLabelControler,'get_isSimFormation',get_isSimFormation)




local util = require 'xlua.util'
xlua.private_accessible(CS.CommonCharacterListLabelHolderController)
local _Open = function(self)
    if self.parentController ~= null and self.parentController.listType == CS.ListType.explore then
    else
    	self:Open();
    end
end
util.hotfix_ex(CS.CommonCharacterListLabelHolderController,'Open',_Open)
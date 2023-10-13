local util = require 'xlua.util'
xlua.private_accessible(CS.SkinDisplayController)
xlua.private_accessible(CS.GashaSkinDisplayController)

local CheckUnloadUnused_New = function(self)
	
end

util.hotfix_ex(CS.SkinDisplayController,'CheckUnloadUnused',CheckUnloadUnused_New)
util.hotfix_ex(CS.GashaSkinDisplayController,'CheckUnloadUnused',CheckUnloadUnused_New)

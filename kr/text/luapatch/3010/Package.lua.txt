local util = require 'xlua.util'
xlua.private_accessible(CS.Package)

local GetisNull = function()
	return false;
end

util.hotfix_ex(CS.Package,'get_isNull',GetisNull)
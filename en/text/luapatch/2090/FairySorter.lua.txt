local util = require 'xlua.util'
xlua.private_accessible(CS.FairySorter)
local _ComparerGet = function(self,left,right)
	 return self:ComparerBase(left.id, right.id);
end
util.hotfix_ex(CS.FairySorter,'ComparerGet',_ComparerGet)
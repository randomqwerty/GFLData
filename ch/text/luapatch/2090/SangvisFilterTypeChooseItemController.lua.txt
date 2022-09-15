local util = require 'xlua.util'
xlua.private_accessible(CS.SangvisFilterTypeChooseItemController)


local _Start = function(self)
	self:Start();

	if self.itemType ==  CS.FilterItemType.level and self.isFullLevel==0 then

		self.isFullLevel=1;
	end
end

 
util.hotfix_ex(CS.SangvisFilterTypeChooseItemController,'Start',_Start)

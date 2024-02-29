local util = require 'xlua.util'
xlua.private_accessible(CS.CommonAttriLayoutController)

local mInitUIElements = function(self)
	if self.listLables.Count >0 then
		self.listLables:Clear()
	end
	self:InitUIElements()
end
local mCloseAllItem = function(self)
	if self.listLables.Count == 0 then
		local len = self.transform.childCount
		for i=0,len-1 do
			self.listLables:Add(self.transform:GetChild(i).gameObject);
		end
	end
	self:CloseAllItem()
end
util.hotfix_ex(CS.CommonAttriLayoutController,'InitUIElements',mInitUIElements)
util.hotfix_ex(CS.CommonAttriLayoutController,'CloseAllItem',mCloseAllItem)
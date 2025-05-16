local util = require 'xlua.util'
xlua.private_accessible(CS.DormVisitorItem)

local Init = function(self,data)
	self:Init(data);
	self.textServerName.text = self.friend.serverName;
end

util.hotfix_ex(CS.DormVisitorItem,'Init',Init)




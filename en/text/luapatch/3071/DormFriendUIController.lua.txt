local util = require 'xlua.util'
xlua.private_accessible(CS.DormFriendUIController)


local Init = function(self)
	self:Init();
	self:ShowFriend(true);
end

local RequestGetFriendListHandler = function(self,result)
	if self.toggleFriend.isOn then
		self:RequestGetFriendListHandler(result);
	else
		CS.DormUIController.Instance:InitFriendList();
	end
end
util.hotfix_ex(CS.DormFriendUIController,'Init',Init)
util.hotfix_ex(CS.DormFriendUIController,'RequestGetFriendListHandler',RequestGetFriendListHandler)



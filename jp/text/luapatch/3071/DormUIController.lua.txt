local util = require 'xlua.util'
xlua.private_accessible(CS.DormUIController)
xlua.private_accessible(CS.DormFriendUIController)

local RequestGetFriendListHandler = function(self,result)
	self:RequestGetFriendListHandler(result);
	CS.DormUIController.Instance:InitFriendList();
end
local needFresh = false;
local needRefresh = function(self)
	if needFresh then
		return true;
	end
	return self.needRefresh;
end

local RequestSelfDormData = function(self,jumpAfterRequest,subJumpType)
	needFresh = false;
	if CS.DormConfigData.instance.currentVisitFriend ~= nil then
		needFresh = true;
	end
	if jumpAfterRequest ~= nil then
		self:RequestSelfDormData(jumpAfterRequest,subJumpType);
	else
		self:RequestSelfDormData();
	end
end

util.hotfix_ex(CS.DormFriendUIController,'RequestGetFriendListHandler',RequestGetFriendListHandler)
util.hotfix_ex(CS.DormConfigData,'get_needRefresh',needRefresh)
util.hotfix_ex(CS.DormUIController,'RequestSelfDormData',RequestSelfDormData)
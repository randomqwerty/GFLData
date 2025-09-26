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

local ShowFriend = function(self,set)
	if set then
		local createConnection = xlua.get_generic_method(CS.ConnectionController, 'CreateConnection');
		local createRequest = createConnection(CS.RequestFriendList);
		createRequest(CS.RequestFriendList(),function(data)
				local generic_method = xlua.get_generic_method(CS.CommonListController, 'InitData');
				local Init = generic_method(CS.Friend);
				Init(self.listController,CS.GameData.listFriend);
				CS.DormUIController.Instance:InitFriendList();
				self.listController.transform.localPosition = CS.UnityEngine.Vector3(0, -100,0);
				if self.goNill ~= nil then
					self.goNill:SetActive(false);
				end
			end);		
	end
end
local InitUI = function(self,isVehicleVisitLog)
	self:InitUI(isVehicleVisitLog);
	if isVehicleVisitLog then
		self.gobjServerNode:SetActive(false);
	end
end
util.hotfix_ex(CS.DormFriendUIController,'RequestGetFriendListHandler',RequestGetFriendListHandler)
util.hotfix_ex(CS.DormConfigData,'get_needRefresh',needRefresh)
util.hotfix_ex(CS.DormUIController,'RequestSelfDormData',RequestSelfDormData)
util.hotfix_ex(CS.DormVehicleVisitLogController,'ShowFriend',ShowFriend)
util.hotfix_ex(CS.DormVehicleVisitorItem,'InitUI',InitUI)
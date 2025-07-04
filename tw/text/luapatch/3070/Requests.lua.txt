local util = require 'xlua.util'
xlua.private_accessible(CS.RequestHomeData)
xlua.private_accessible(CS.Friend)

local EnterIntoList = function(self,friendType)
	if self.uid == 0 then
		return;
	end
	self:EnterIntoList(friendType);
end
local SuccessJsonHandleData = function(self,jsonData)	
	self:SuccessJsonHandleData(jsonData);
	if CS.HotUpdateController.instance.mUsePlatform ~= CS.HotUpdateController.EUsePlatform.ePlatform_Normal then
		if jsonData:Contains("friend_applylist") then
			local json = jsonData:GetValue("friend_applylist");
			CS.GameData.listFriendApplied:Clear();
			for i=0,json.Count-1 do
				local friend = CS.Friend(json[i]);
				friend:EnterIntoList(CS.FriendType.BeAppliedStranger);
			end
		end
	end
end
util.hotfix_ex(CS.RequestHomeData,'SuccessJsonHandleData',SuccessJsonHandleData)
util.hotfix_ex(CS.Friend,'EnterIntoList',EnterIntoList)

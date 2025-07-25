local util = require 'xlua.util'
xlua.private_accessible(CS.Data)
xlua.private_accessible(CS.GameFunctionSwitch)
xlua.private_accessible(CS.Friend)

local UserExistsSkin = function(package)
	local choose = false;
	local presentInfo = nil;
	for i=0,CS.GameData.listPresentInfo.Count-1 do
		local info = CS.GameData.listPresentInfo[i];
		if info.prize_id == package.id then
			presentInfo = info;
		end
	end
	CS.NDebug.Log("id",package.id);
	if presentInfo ~= nil and presentInfo.presentType == CS.PresentInfo.PresentType.Optional then
		choose = true;
	end
	if choose and package:HasGiftPackage() then
		local has = true;
		CS.NDebug.Log("当前自选礼包");
		for i=0,package.listGiftPackage.Count-1 do
			local info = package.listGiftPackage[i].info;
			if info ~= nil then
				local skinId = info.id;
				if skinId ~= 0 then
					local e = CS.GameData.listSkin:Exists(function(g)
						return g.info.id == skinId;
					end) 
					local e1 = CS.GameData.listGift:Exists(function(g)
						return g.info.skin == skinId;
					end)
					if not e and not e1 then
						CS.NDebug.Log("未拥有皮肤",skinId);
						has = false;
					end
				end
			end
		end
		return has;
	else
		return CS.Data.UserExistsSkin(package);
	end
end

local Description = function(self)
	return self:DescriptionOnSelect();
end

local EnterIntoList = function(self,friendType)
	self.friendStatus = friendType;
	local id = self:GetID();
	if friendType == CS.FriendType.Friend then
		if not CS.GameData.listFriend:ContainsKey(id) then
			CS.GameData.listFriend:Add(self);
		end
	elseif friendType == CS.FriendType.BlackList then
		if not CS.GameData.listBlackList:ContainsKey(id) then
			CS.GameData.listBlackList:Add(self);
		end
	elseif friendType == CS.FriendType.RandomStranger then
		if not CS.GameData.listRandomFriend:ContainsKey(id) then
			CS.GameData.listRandomFriend:Add(self);
		end
	elseif friendType == CS.FriendType.BeAppliedStranger then
		if not CS.GameData.listFriendApplied:ContainsKey(id) then
			CS.GameData.listFriendApplied:Add(self);
		end
	elseif friendType == CS.FriendType.ApplyingStranger then
		if not CS.GameData.listFriendApplying:ContainsKey(id) then
			CS.GameData.listFriendApplying:Add(self);
		end
	elseif friendType == CS.FriendType.SearchList then
		if not CS.GameData.listSearchFriend:ContainsKey(id) then
			CS.GameData.listSearchFriend:Add(self);
		end
	end
end
util.hotfix_ex(CS.Data,'UserExistsSkin',UserExistsSkin)
util.hotfix_ex(CS.GameFunctionSwitch,'Description',Description)
util.hotfix_ex(CS.Friend,'EnterIntoList',EnterIntoList)

local util = require 'xlua.util'
xlua.private_accessible(CS.Data)
xlua.private_accessible(CS.Friend)

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
local engagedSpot = function()
	local spot = CS.GameData.engagedSpot;
	if spot == nil then
		for i=0,CS.GameData.listSpotAction.Count-1 do
			local spotaction = CS.GameData.listSpotAction:GetDataByIndex(i);
			if spotaction.CannotSee then
				local hasFriend = false;
				local hasEnemy = false;
				if spotaction.friendlyTeamId ~= 0 or spotaction.sangvisTeamId ~= 0 or spotaction.vehicleTeamID ~= 0 then
					hasFriend = true;
				end
				if spotaction.enemyInstanceId ~= 0 or spotaction.enemyTeamId ~= 0 then
					hasEnemy = true;
				end
				for j=0,spotaction.allyTeamInstanceIds.Count-1 do
					local allyteam = CS.GameData.missionAction.listAllyTeams:GetDataById(spotaction.allyTeamInstanceIds[j]);
					if allyteam ~= nil then
						if allyteam.currentBelong == CS.TeamBelong.friendly then
							hasFriend = true;
						else
							hasEnemy = true;
						end
					end
				end
				if hasFriend and hasEnemy then
					CS.DeploymentController.lastEngageSpotId = spotaction.spotInfo.id;
					return spotaction;
				end
			end
		end
	end
	return spot;
end
util.hotfix_ex(CS.Friend,'EnterIntoList',EnterIntoList)
util.hotfix_ex(CS.GameData,'get_engagedSpot',engagedSpot)
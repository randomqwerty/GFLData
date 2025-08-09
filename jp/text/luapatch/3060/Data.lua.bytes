local util = require 'xlua.util'
xlua.private_accessible(CS.Data)

local GetAdjutantSlotPosInfos = function()

	local adjutantConfig = CS.UnityEngine.PlayerPrefs.GetString("localAdjutantSlotPosInfo"); 
	local vecConfigs = Split(adjutantConfig, ",")
	local newConfig = ""

	for i=1, #vecConfigs do
		if vecConfigs[i] == ""then
			local index = i - 1
			newConfig = newConfig ..tostring(index).."||0|False|0_0_0|0_0_0"
		else
			newConfig = newConfig .. vecConfigs[i]
		end

		if i ~= #vecConfigs then        
            newConfig = newConfig .. ","
        end 
	end

	CS.UnityEngine.PlayerPrefs.SetString("localAdjutantSlotPosInfo", newConfig);
	CS.Data.GetAdjutantSlotPosInfos()
end

function Split(szFullString, szSeparator)
	if(szFullString == nil) then
		return nil
	end
	local nFindStartIndex = 0
	local nSplitIndex = 1
	local nSplitArray = {}
	while true do
		local nFindLastIndex = string.find(szFullString, szSeparator, nFindStartIndex)
		if not nFindLastIndex then
			nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, string.len(szFullString))
			break
		end
		nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, nFindLastIndex - 1)
		nFindStartIndex = nFindLastIndex + string.len(szSeparator)
		nSplitIndex = nSplitIndex + 1
	end
	return nSplitArray
end

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

local UseNewDailyLimit = function(self)
	if self.iteamInfo == nil then
		return false;
	end
	return self.UseNewDailyLimit;
end
local day = function(self)
	if self.iteamInfo == nil then
		return false;
	end
	return self.day;
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
util.hotfix_ex(CS.Data,'GetAdjutantSlotPosInfos',GetAdjutantSlotPosInfos)
util.hotfix_ex(CS.Data,'UserExistsSkin',UserExistsSkin)
util.hotfix_ex(CS.ItemLimit,'get_UseNewDailyLimit',UseNewDailyLimit)
util.hotfix_ex(CS.ItemLimit,'get_day',day)
util.hotfix_ex(CS.GameData,'get_engagedSpot',engagedSpot)


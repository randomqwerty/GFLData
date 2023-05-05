local util = require 'xlua.util'
xlua.private_accessible(CS.OPSTowerMissionConfig)

local CheckScrollIndexPos = function(self,index,play,delay)
	local posy = self.baseHeight - self.itemHeight * index;
	local offset = self.opsTowerMissions[index].offset;
	posy = posy-offset.y;
	if play then
		self.scrollect.content:DOKill();
		self.scrollect.content:DOAnchorPosY(posy, self.durationTime):SetDelay(delay):SetEase(CS.DG.Tweening.Ease.OutQuad);
	else
		self.scrollect.content.anchoredPosition = CS.UnityEngine.Vector2(0,posy);
	end
end

local ClearCount = function(self)
	if self.entranceId ~= 0 then
		if CS.OPSConfig.missionEntranceInfos:ContainsKey(self.entranceId) then
			return 0;
		else
			local info = CS.OPSConfig.missionEntranceInfos[self.entranceId];
			if info.index == -1 then
				return 1;
			end
		end
	else
		for i=0,self.missionIds.Count-1 do
			local mission = CS.GameData.listMission:GetDataById(self.missionIds[i]);
			if mission ~= nil then
				if mission.missionInfo.isEndless then
					if mission.counter>0 then
						return 1;
					end
				elseif mission.missionInfo.specialType ~= CS.MapSpecialType.Story then
					if mission.UseWinCounter > 0 then
						return 1;
					end
				elseif mission.missionInfo.specialType == CS.MapSpecialType.Story then
					if mission.counter > 0 then
						return 1;
					end
				end
			end
		end
	end
	return 0;
end
local AllCount = function(self)
	return 1;
end
util.hotfix_ex(CS.OPSTowerMissionConfig,'CheckScrollIndexPos',CheckScrollIndexPos)
util.hotfix_ex(CS.OPSMission,'ClearCount',ClearCount)
util.hotfix_ex(CS.OPSMission,'AllCount',AllCount)

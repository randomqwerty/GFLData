local util = require 'xlua.util'
xlua.private_accessible(CS.OPSMission)

local HasUnBattleMission = function(self)
	if self.entranceId ~= 0 then
		return self:HasUnBattleMission();
	else
		local diffcluty = CS.OPSPanelController.difficulty;	
		for i=0,self.missionIds.Count -1 do
			local missionid = self.missionIds[i];
			if diffcluty == i then
				local mission = CS.GameData.listMission:GetDataById(missionid);
				if mission ~= nil then
					if mission.missionInfo.specialType ~= CS.MapSpecialType.Story then
						if mission.missionInfo.isEndless then
							return mission.counter == 0;
						else
							return mission.UseWinCounter == 0;
						end
					else
						return mission.counter == 0;
					end
				end
			end
		end
	end
end

local CurrentMissionId = function(self)
	if self.entranceId == 0 then
		if self.missionIds.Count > 0 then
			local diff = CS.Mathf.Clamp(CS.OPSPanelController.difficulty,0,self.missionIds.Count-1);
			return self.missionIds[diff];
		end
		return 0;
	else
		return CS.OPSPanelController.Instance:GetCurrentMissionId(self.entranceId);
	end	
end
util.hotfix_ex(CS.OPSMission,'HasUnBattleMission',HasUnBattleMission)
util.hotfix_ex(CS.OPSMission,'get_CurrentMissionId',CurrentMissionId)





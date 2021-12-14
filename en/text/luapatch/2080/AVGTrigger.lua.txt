local util = require 'xlua.util'
xlua.private_accessible(CS.AVGTrigger)

local PlayMissionEndWinAVG = function(self)
	self.scriptName = nil;
	local check = false;
	local mission = CS.GameData.listMission:GetDataById(CS.GameData.currentSelectedMissionInfo.id);
	if mission.medal1 and mission.winCount == 1 then
		mission.medal1 = false;
		check = true;
	end
	self:PlayMissionEndWinAVG();
	if check then
		mission.medal1 = true;
	end
end

local ScriptName = function(self,currentMission,script)
	if currentMission.winCount == 1 and CS.GameData.missionResult ~= nil then
		self:ScriptEndName(script);
		return;
	end
	self:ScriptName(currentMission,script);
end
util.hotfix_ex(CS.AVGTrigger,'PlayMissionEndWinAVG',PlayMissionEndWinAVG)
util.hotfix_ex(CS.AVGTrigger,'ScriptName',ScriptName)
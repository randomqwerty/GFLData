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

util.hotfix_ex(CS.AVGTrigger,'PlayMissionEndWinAVG',PlayMissionEndWinAVG)
local util = require 'xlua.util'
xlua.private_accessible(CS.MotherBaseController)

local ShowSpecialEffect = function(self)
	local missionId = CS.Data.GetInt("motherbase_bombing_switch", 0);
	local mission = CS.GameData.listMission:GetDataById(missionId);
	if mission ~= nil and mission.UseWinCounter == 0 then
		return;
	end
	self:ShowSpecialEffect();
end

util.hotfix_ex(CS.MotherBaseController,'ShowSpecialEffect',ShowSpecialEffect)


local util = require 'xlua.util'
xlua.private_accessible(CS.OPSPanelController)

slectMissionId = 0;

local CannotShow = function(self,mission)
	if slectMissionId ~= 0 then
		return false;
	end
	return self:CannotShow(mission);
end
local DoSomethingNextFrame= function(self)
	if slectMissionId == 0 then
		return;
	end
	local mission = CS.GameData.listMission:GetDataByID(slectMissionId);
	if mission == nil then
		slectMissionId = 0;
		return;
	end
	self:InitProcessData();
	for i=0,self.processInfos.Count-1 do
		if self.processInfos[i].mission == mission then
			self.showprocess = true;
			self:SelectProcessInfo(self.processInfos[i]);
		end
	end
	slectMissionId = 0;
end

util.hotfix_ex(CS.OPSPanelController,'CannotShow',CannotShow)
util.hotfix_ex(CS.OPSPanelController,'DoSomethingNextFrame',DoSomethingNextFrame)